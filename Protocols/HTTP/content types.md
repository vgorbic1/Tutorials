## Representing Content Types

The `Content-Type` header in an HTTP request or response describes the content type for the message
body. The `Accept` header in the request tells the server the content types that the client is expecting in
the response body. The content types are represented using the Internet media type. The Internet media
type (also known as the MIME type) indicates the type of data that a file contains.
```
Content-Type: text/html
```
The format of the content
type values is a primary type/subtype followed by an optional semicolon delimited attribute-value
pairs (known as parameters).

- `text:` This type indicates that the content is plain text and no special software is required to read the 
contents. The subtype represents more specific details about the content, which can be used
by the client for special processing, if any. For instance, `Content-Type: text/html` indicates
that the body content is html, and the client can use this hint to kick off an appropriate rendering
engine while displaying the response.
- `multipart:` As the name indicates, this type consists of multiple parts of the independent data
types. For instance,` Content-Type: multipart/form-data` is used for submitting forms that
contain the files, non-ASCII data, and binary data.
- `message:` This type encapsulates more messages. It allows messages to contain other messages
or pointers to other messages. For instance, the `Content-Type: message/partial` content
type allows for large messages to be broken up into smaller messages. The full message can then
be read by the client (user agent) by putting all the broken messages together.
- `image:` This type represents the image data. For instance, `Content-Type: image/png` indicates
that the body content is a .png image.
- `audio:` This type indicates the audio data. For instance, `Content-Type: audio/mpeg` indicates
that the body content is MP3 or other MPEG audio.
- `video:` This type indicates the video data. For instance, `Content-Type: video/mp4` indicates
that the body content is MP4 video.
- `application:` This type represents the application data or binary data. For instance, `Content-
Type: application/json; charset=utf-8` designates the content to be in the JavaScript
Object Notation (JSON) format, encoded with UTF-8 character encoding.

Refer to the [complete list](http://www.iana.org/assignments/media-types/media-types.xhtml).
