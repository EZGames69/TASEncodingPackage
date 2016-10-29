# tested on AviSynth 2.6 alpha 3

LoadCPlugin ("freesub.dll")


FreeSub (clip, string "text", int "x", int "y", int "first_frame", int "last_frame", string "font", int "size", int "text_color", int "halo_color", int "align", int "lsp", int "font_width", int "halo_width", int "halo_height")



clip [unnamed] (no default)
Clip to overlay on.  Supported formats are RGB24, RGB32, YV24.  Overlay engine is lossless on all pixels that don't have text or halo on them.
BUG: Don't try to feed it I420!!!! Trust me.

string text (default "The quick brown fox jumps over the lazy dog.")
Text to write.  UTF-8 (should?) be supported.  In multiline mode, newline in string and "\n" escape sequence are both interpreted as newline.  In this mode, "\\" displays a single '\'.  There are no escape sequences in single line mode.

int x (default center of clip)
int y (default center of clip)
Anchor point.  Actual position of text also depends on alignment.

int first_frame (default 0)
int last_frame (default last frame of clip)
Frames to display subtitle on, inclusive.

string font (default "default.bdf")
Path to BDF font file.  Can be relative to script location, like most script paths.

int size (default 1)
Scales the height of the text by an integer multiple of its original size using a point resize.  Not quite the same as Subtitle() size since overall size also depends on the original font size.

int text_color (default #20ffffff)
Text color.  When viewed as big endian, the bytes are ARGB in RGB24/RGB32 mode, and AYVU in YV24 mode.  For alpha, #00 is opaque and #ff is exactly transparent.  The other color intensities depend on the interpretation of the space, including things like range and YCbCr matrix.

int halo_color (default #20000000)
As above, but for a border around the text.

int align (default 5)
Controls the position of the text relative to the anchor point.  1,4,7 are left aligned to the right of the anchor point.  2,5,8 are centered (left to right) on the anchor point.  3,6,9 are right aligned to the left of the anchor point.  1,2,3 are bottom aligned to the top of the anchor point.  4,5,6 are centered (top to bottom) on the anchor point.  7,8,9 are top aligned to the bottom of the anchor point.  Look at a numpad, not a telephone pad.

int lsp (default unset)
Setting any value for this turns on multiline mode, which displays multiple line text.  Align properly understands this in both x and y directions.  0 uses the default line spacing.  negative values put lines of text closer together, which can cause overwriting if things are too close.  Positive values put the lines of text farther apart.  These units are multiplied by "size".

int font_width (default same as size)
Like "size", but in the horizontal direction.

int halo_width (default same as font_width)
Draws a border around the text with this width.  Setting 0 effectively disables the border on the sides of text.

int halo_height (default same as size)
Draws a border around the text with this height.  Setting 0 effectively disables the border on the top and bottom of text.  If both halo_width and halo_height are 0, there will be no border.

