---
layout: post
title: 'Async File System Watcher'
tags: [csharp]
---

The `FileSystemWatcher` class in .NET predates the asyncy goodness introduced in later framework versions. Here's an async version implemented by subscribing to a wrapped watcher's `Created` event. Note - you might additionally want to subscribe to the `Renamed` event, I've omitted it from the example for brevity.

~~~csharp
sealed class AsyncFileSystemWatcher : IDisposable
{
    readonly FileSystemWatcher _fileSystemWatcher;
    readonly string _directoryPath;

    public AsyncFileSystemWatcher(string directoryPath)
    {
        _fileSystemWatcher = new FileSystemWatcher(directoryPath) 
		{ 
		    EnableRaisingEvents = true 
        };
        _directoryPath = directoryPath;
    }

    public Task WaitForFileCreationAsync(string fileName)
    {
        if (string.IsNullOrWhiteSpace(fileName))
            throw new ArgumentException("Cannot be null or whitespace.", nameof(fileName));
       
        var taskSource = new TaskCompletionSource<bool>();

        _fileSystemWatcher.Created += (obj, args) =>
        {
            if (args.Name == Path.GetFileName(fileName))
            {
                taskSource.TrySetResult(true);
            }
        };
        
        // need to check if the file has already been created
        if (File.Exists(Path.Combine(_directoryPath, fileName)))
            taskSource.TrySetResult(true);

        return taskSource.Task;
    }

    public void Dispose()
    {
        _fileSystemWatcher.Dispose();
    }
}
~~~

Example usage:

~~~csharp
using (var watcher = new AsyncFileSystemWatcher(@"C:\temp"))
{
    await watcher.WaitForFileCreationAsync("test.txt");
    // do whatever...
}
~~~


