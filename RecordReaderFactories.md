| **Class** | **Description** |
|:----------|:----------------|
| [FileLengthRecordReaderFactory](http://github.com/born2snipe/flapjack/blob/8552771b7e860dc9fc7b2fdef01e4d252d398819/flapjack/src/main/java/flapjack/io/FileLengthRecordReaderFactory.java) | Creates either a MappedRecordReader or a NioRecordReader depending on the file size that is about to be processed. The file length to toggle between the two implementations is configurable. |
| [FileStreamRecordReaderFactory](http://github.com/born2snipe/flapjack/blob/8552771b7e860dc9fc7b2fdef01e4d252d398819/flapjack/src/main/java/flapjack/io/FileStreamRecordReaderFactory.java) | Creates a RecordReader that uses that Java IO stream |
| [LineRecordReaderFactory](http://github.com/born2snipe/flapjack/blob/8552771b7e860dc9fc7b2fdef01e4d252d398819/flapjack/src/main/java/flapjack/io/LineRecordReaderFactory.java) | Creates a RecordReader that uses the line endings to signal as the record terminator |
| [MappedRecordReaderFactory](http://github.com/born2snipe/flapjack/blob/8552771b7e860dc9fc7b2fdef01e4d252d398819/flapjack/src/main/java/flapjack/io/MappedRecordReaderFactory.java) |  Creates a RecordReader which is using the Java NIO mapped file api |
| [NioRecordReaderFactory](http://github.com/born2snipe/flapjack/blob/8552771b7e860dc9fc7b2fdef01e4d252d398819/flapjack/src/main/java/flapjack/io/NioRecordReaderFactory.java) | Creates a RecordReader that is using the Java NIO file api |