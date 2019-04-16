# zip

```
import "archive/zip"
```

源码
+ [struct.go](https://golang.google.cn/src/archive/zip/struct.go)
+ [register.go](https://golang.google.cn/src/archive/zip/register.go)
+ [reader.go](https://golang.google.cn/src/archive/zip/reader.go)
+ [writer.go](https://golang.google.cn/src/archive/zip/writer.go)

目录
+ [概述](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#%E6%A6%82%E8%BF%B0)
+ [常量](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#%E5%B8%B8%E9%87%8F)
+ [变量](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#%E5%8F%98%E9%87%8F)
+ [方法](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#%E6%96%B9%E6%B3%95)
    + [RegisterCompressor](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#registercompressor)
    + [RegisterDecompressor](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#registerdecompressor)
    + [FileInfoHeader](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#fileinfoheader)
    + [OpenReader](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#openreader)
    + [NewReader](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#newreader)
    + [NewWriter](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#newwriter)
+ [Compressor](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#compressor)
+ [Decompressor](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#decompressor)
+ [File](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#file)
    + [File.DataOffset](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#filedataoffset)
    + [File.Open](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#fileopen)
+ [FileHeader](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#fileheader)
    + [FileHeader.FileInfo](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#fileheaderfileinfo)
    + [FileHeader.ModTime](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#fileheadermodtime)
    + [FileHeader.Mode](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#fileheadermode)
    + [FileHeader.SetModTime](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#fileheadersetmodtime)
    + [FileHeader.SetMode](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#fileheadersetmode)
+ [ReadCloser](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#readcloser)
    + [ReadCloser.Close](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#readcloserclose)
+ [Reader](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#reader)
    + [Reader.RegisterDecompressor](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#readerregisterdecompressor)
+ [Writer](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writer)
    + [Writer.Create](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writercreate)
    + [Writer.CreateHeader](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writercreateheader)
    + [Writer.RegisterCompressor](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writerregistercompressor)
    + [Writer.Flush](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writerflush)
    + [Writer.Close](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writerclose)
    + [Writer.SetComment](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writersetcomment)
    + [Writer.SetOffset](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writersetoffset)
+ [示例](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#%E7%A4%BA%E4%BE%8B)
    + [Reader](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#reader-1)
    + [Writer](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writer-1)
    + [Writer.RegisterCompressor](https://github.com/freejee/topics/blob/master/golang/packages/zip.md#writerregistercompressor-1)

## 概述

Package zip provides support for reading and writing ZIP archives.

See: https://www.pkware.com/appnote

This package does not support disk spanning.

A note about ZIP64: 

To be backwards compatible the FileHeader has both 32 and 64 bit Size fields.

The 64 bit fields will always contain the correct value and for normal archives both fields will be the same.

For files requiring the ZIP64 format the 32 bit fields will be 0xffffffff and the 64 bit fields must be used instead.

## 常量

```
const (
    Store   uint16 = 0 // no compression
    Deflate uint16 = 8 // DEFLATE compressed
)
```

Compression methods.

## 变量

```
var (
    ErrFormat    = errors.New("zip: not a valid zip file")
    ErrAlgorithm = errors.New("zip: unsupported compression algorithm")
    ErrChecksum  = errors.New("zip: checksum error")
)
```

## 方法

### RegisterCompressor

```
func RegisterCompressor(method uint16, comp Compressor)
```

RegisterCompressor registers custom compressors for a specified method ID.

The common methods Store and Deflate are built in.

### RegisterDecompressor

```
func RegisterDecompressor(method uint16, dcomp Decompressor)
```

RegisterDecompressor allows custom decompressors for a specified method ID.

The common methods Store and Deflate are built in.

### FileInfoHeader

```
func FileInfoHeader(fi os.FileInfo) (*FileHeader, error)
```

FileInfoHeader creates a partially-populated FileHeader from an os.FileInfo.

Because os.FileInfo's Name method returns only the base name of the file it describes, it may be necessary to modify the Name field of the returned header to provide the full path name of the file.

If compression is desired, callers should set the FileHeader.Method field; it is unset by default.

### OpenReader

```
func OpenReader(name string) (*ReadCloser, error)
```

OpenReader will open the Zip file specified by name and return a ReadCloser.

### NewReader

```
func NewReader(r io.ReaderAt, size int64) (*Reader, error)
```

NewReader returns a new Reader reading from r, which is assumed to have the given size in bytes.

### NewWriter

```
func NewWriter(w io.Writer) *Writer
```

NewWriter returns a new Writer writing a zip file to w.

## Compressor

```
type Compressor func(w io.Writer) (io.WriteCloser, error)
```

A Compressor returns a new compressing writer, writing to w.

The WriteCloser's Close method must be used to flush pending data to w.

The Compressor itself must be safe to invoke from multiple goroutines simultaneously, but each returned writer will be used only by one goroutine at a time.

## Decompressor

```
type Decompressor func(r io.Reader) io.ReadCloser
```

A Decompressor returns a new decompressing reader, reading from r.

The ReadCloser's Close method must be used to release associated resources.

The Decompressor itself must be safe to invoke from multiple goroutines simultaneously, but each returned reader will be used only by one goroutine at a time.

## File

```
type File struct {
    FileHeader
    // contains filtered or unexported fields
}
```

### File.DataOffset

```
func (f *File) DataOffset() (offset int64, err error)
```

DataOffset returns the offset of the file's possibly-compressed data, relative to the beginning of the zip file.

Most callers should instead use Open, which transparently decompresses data and verifies checksums.

### File.Open

```
func (f *File) Open() (io.ReadCloser, error)
```

Open returns a ReadCloser that provides access to the File's contents.

Multiple files may be read concurrently.

## FileHeader

```
type FileHeader struct {
    // Name is the name of the file.
    // It must be a relative path, not start with a drive letter (such as "C:"), and must use forward slashes instead of back slashes.
    // A trailing slash indicates that this file is a directory and should have no data.
    // When reading zip files, the Name field is populated from the zip file directly and is not validated for correctness.
    // It is the caller's responsibility to sanitize it as appropriate, including canonicalizing slash directions, validating that paths are relative, and preventing path traversal through filenames ("../../../").
    Name string

    // Comment is any arbitrary user-defined string shorter than 64KiB.
    Comment string

    // NonUTF8 indicates that Name and Comment are not encoded in UTF-8.
    // By specification, the only other encoding permitted should be CP-437, but historically many ZIP readers interpret Name and Comment as whatever the system's local character encoding happens to be.
    // This flag should only be set if the user intends to encode a non-portable ZIP file for a specific localized region.
    // Otherwise, the Writer automatically sets the ZIP format's UTF-8 flag for valid UTF-8 strings.
    NonUTF8 bool // Go 1.10

    CreatorVersion uint16
    ReaderVersion  uint16
    Flags          uint16

    // Method is the compression method. If zero, Store is used.
    Method uint16

    // Modified is the modified time of the file.
    // When reading, an extended timestamp is preferred over the legacy MS-DOS date field, and the offset between the times is used as the timezone.
    // If only the MS-DOS date is present, the timezone is assumed to be UTC.
    // When writing, an extended timestamp (which is timezone-agnostic) is always emitted.
    // The legacy MS-DOS date field is encoded according to the location of the Modified time.
    Modified     time.Time    // Go 1.10
    ModifiedTime uint16       // Deprecated: Legacy MS-DOS date; use Modified instead.
    ModifiedDate uint16       // Deprecated: Legacy MS-DOS time; use Modified instead.

    CRC32              uint32
    CompressedSize     uint32 // Deprecated: Use CompressedSize64 instead.
    UncompressedSize   uint32 // Deprecated: Use UncompressedSize64 instead.
    CompressedSize64   uint64 // Go 1.1
    UncompressedSize64 uint64 // Go 1.1
    Extra              []byte
    ExternalAttrs      uint32 // Meaning depends on CreatorVersion
}
```

FileHeader describes a file within a zip file.

See the zip spec for details.

### FileHeader.FileInfo

```
func (h *FileHeader) FileInfo() os.FileInfo
```

FileInfo returns an os.FileInfo for the FileHeader.

### FileHeader.ModTime

```
func (h *FileHeader) ModTime() time.Time
```

ModTime returns the modification time in UTC using the legacy ModifiedDate and ModifiedTime fields.

Deprecated: Use Modified instead.

### FileHeader.Mode

```
func (h *FileHeader) Mode() (mode os.FileMode)
```

Mode returns the permission and mode bits for the FileHeader.

### FileHeader.SetModTime

```
func (h *FileHeader) SetModTime(t time.Time)
```

SetModTime sets the Modified, ModifiedTime, and ModifiedDate fields to the given time in UTC.

Deprecated: Use Modified instead.

### FileHeader.SetMode

```
func (h *FileHeader) SetMode(mode os.FileMode)
```

SetMode changes the permission and mode bits for the FileHeader.

## ReadCloser

```
type ReadCloser struct {
    Reader
    // contains filtered or unexported fields
}
```

### ReadCloser.Close

```
func (rc *ReadCloser) Close() error
```

Close closes the Zip file, rendering it unusable for I/O.

## Reader

```
type Reader struct {
    File    []*File
    Comment string
    // contains filtered or unexported fields
}
```

### Reader.RegisterDecompressor

```
func (z *Reader) RegisterDecompressor(method uint16, dcomp Decompressor)
```

RegisterDecompressor registers or overrides a custom decompressor for a specific method ID.

If a decompressor for a given method is not found, Reader will default to looking up the decompressor at the package level.

## Writer

```
type Writer struct {
    // contains filtered or unexported fields
}
```

Writer implements a zip file writer.

### Writer.Create

```
func (w *Writer) Create(name string) (io.Writer, error)
```

Create adds a file to the zip file using the provided name.

It returns a Writer to which the file contents should be written.

The file contents will be compressed using the Deflate method.

The name must be a relative path: it must not start with a drive letter (e.g. C:) or leading slash, and only forward slashes are allowed.

To create a directory instead of a file, add a trailing slash to the name.

The file's contents must be written to the io.Writer before the next call to Create, CreateHeader, or Close.

### Writer.CreateHeader

```
func (w *Writer) CreateHeader(fh *FileHeader) (io.Writer, error)
```

CreateHeader adds a file to the zip archive using the provided FileHeader for the file metadata.

Writer takes ownership of fh and may mutate its fields.

The caller must not modify fh after calling CreateHeader.

This returns a Writer to which the file contents should be written.

The file's contents must be written to the io.Writer before the next call to Create, CreateHeader, or Close.

### Writer.RegisterCompressor

```
func (w *Writer) RegisterCompressor(method uint16, comp Compressor)
```

RegisterCompressor registers or overrides a custom compressor for a specific method ID.

If a compressor for a given method is not found, Writer will default to looking up the compressor at the package level.

### Writer.Flush

```
func (w *Writer) Flush() error
```

Flush flushes any buffered data to the underlying writer.

Calling Flush is not normally necessary; calling Close is sufficient.

### Writer.Close

```
func (w *Writer) Close() error
```

Close finishes writing the zip file by writing the central directory.

It does not close the underlying writer.

### Writer.SetComment

```
func (w *Writer) SetComment(comment string) error
```

SetComment sets the end-of-central-directory comment field.

It can only be called before Close.

### Writer.SetOffset

```
func (w *Writer) SetOffset(n int64)
```

SetOffset sets the offset of the beginning of the zip data within the underlying writer.
 
It should be used when the zip data is appended to an existing file, such as a binary executable.

It must be called before any data is written.

## 示例

### Reader

```
package main

import (
    "archive/zip"
    "fmt"
    "io"
    "log"
    "os"
)

func main() {
    // Open a zip archive for reading.
    r, err := zip.OpenReader("testdata/readme.zip")
    if err != nil {
        log.Fatal(err)
    }
    defer r.Close()

    // Iterate through the files in the archive, printing some of their contents.
    for _, f := range r.File {
        fmt.Printf("Contents of %s:\n", f.Name)
        rc, err := f.Open()
        if err != nil {
            log.Fatal(err)
        }
        _, err = io.CopyN(os.Stdout, rc, 68)
        if err != nil {
            log.Fatal(err)
        }
        rc.Close()
        fmt.Println()
    }
}
```

### Writer

```
package main

import (
    "archive/zip"
    "bytes"
    "log"
)

func main() {
    // Create a buffer to write our archive to.
    buf := new(bytes.Buffer)

    // Create a new zip archive.
    w := zip.NewWriter(buf)

    // Add some files to the archive.
    var files = []struct {
        Name, Body string
    }{
        {"readme.txt", "This archive contains some text files."},
        {"gopher.txt", "Gopher names:\nGeorge\nGeoffrey\nGonzo"},
        {"todo.txt", "Get animal handling licence.\nWrite more examples."},
    }
    for _, file := range files {
        f, err := w.Create(file.Name)
        if err != nil {
            log.Fatal(err)
        }
        _, err = f.Write([]byte(file.Body))
        if err != nil {
            log.Fatal(err)
        }
    }

    // Make sure to check the error on Close.
    err := w.Close()
    if err != nil {
        log.Fatal(err)
    }
}
```

### Writer.RegisterCompressor

```
package main

import (
    "archive/zip"
    "bytes"
    "compress/flate"
    "io"
)

func main() {
    // Override the default Deflate compressor with a higher compression level.

    // Create a buffer to write our archive to.
    buf := new(bytes.Buffer)

    // Create a new zip archive.
    w := zip.NewWriter(buf)

    // Register a custom Deflate compressor.
    w.RegisterCompressor(zip.Deflate, func(out io.Writer) (io.WriteCloser, error) {
        return flate.NewWriter(out, flate.BestCompression)
    })

    // Proceed to add files to w.
}
```


