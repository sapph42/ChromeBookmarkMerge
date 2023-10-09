# ChromiumBookmarkManager

## BookmarkFile

### Definition

Namespace: ChromiumBookmarkManager  
Assembly: ChromeBookmarkMerge.dll

Provides method for merging two Chromium Bookmark files (version 1, JSON).

    public class BookmarkFile
	
### Examples

The following example demonstrates the methods of the BookmarkFile class.

    using ChromiumBookmarkManager;
	
    class Test {
        public static void Main() {
            string LiveBookmarks = "C:\Users\You\AppData\Local\Google\Chrome\User Data\Default\Bookmarks";
            var file1 = new BookmarkFile(LiveBookmarks);
            var file2 = new BookmarkFile("C:\Users\You\Documents\Backup\Bookmarks");
			var file3 = file1.Merge(file2);
            foreach (Process chromeproc in Process.GetProcessesByName("chrome")) {
                chromeproc.Kill();
                chromeproc.WaitForExit();
            }
            file3.WriteFile(LiveBookmarks);
        }
    }

## BookmarkFile Constructors

### Definition

Namespace: ChromiumBookmarkManager  
Assembly: ChromeBookmarkMerge.dll

Initializes a new instance of the BookmarkFile class.

#### BookmarkFile()

Initializes a new instance of the BookmarkFile class without a reference to the file system.

#### BookmarkFile(string)

Initializes a new instance of the BookmarkFile class based on a valid filesystem path provided in the string parameter.

##### Parameters

`BookmarkFilePath` string 

The fully qualified name of the new file, or the relative file name. Do not end the path with the directory separator character. 

## BookmarkFile.Merge 

### Definition

Namespace: ChromiumBookmarkManager  
Assembly: ChromeBookmarkMerge.dll

Merges this instance of BookmarkFile with another.

#### Merge(BookmarkFile)

    public BookmarkFile? Merge(BookmarkFile OtherFile);

##### Parameters

`OtherFile` BookmarkFile

The other Chromium JSON Version 1 bookmark file that will be merged with this object.

##### Returns

BookmarkFile?

A new BookmarkFile object with the merged data from the original object and parameter object.  Will be null under the following conditions

1. BookmarkFilePath property on either object is not set.
2. Filesystem object referenced by BookmarkFilePath property on either object does not exist.
3. Filesystem object referenced by BookmarkFilePath property on either object is not accessible.
4. JSON parsing fails on bookmark file referenced by BookmarkFilePath property on either object.

## BookmarkFile.WriteFile

### Definition

Namespace: ChromiumBookmarkManager  
Assembly: ChromeBookmarkMerge.dll

Writes the JSON data associated with this object to the filesystem object referenced.

#### WriteFile()

    public void WriteFile();
	
Writes the JSON data in this object to the filesystem object referenced by the object's BookmarkFilePath.

#### WriteFile(string)

    public void WriteFile(string file_name)
	
Writes the JSON data in this object to the file system object referenced by the file_name parameter.

##### Parameters

`file_name` String

A valid filesystem path.

##### Exceptions

NullReferenceException  
No JSON data loaded in BookmarkFile object

NullReferenceException  
file_name and BookmarkFilePath are both null.

IOException  
.NET 8 and later versions: The underlying pipe is closed or disconnected.

##### Remarks

WriteFile will destructively overwrite any existing file at the path provided.