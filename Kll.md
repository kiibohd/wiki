Currently, the only way to define keyboard layouts is using [KLL](http://input.club/kll), the Keyboard Layout Language.

> KLL outlines a complex keymapping scheme for custom keyboard firmware.
> It is based upon the concept of trigger:result pairs and ways to configure both parts of the pair (input and output).
> A variety of macros are supported along with analog keyswitches.
> In addition, this keymapping scheme supports static and dynamic layering as well as supporting arbitrary keyboard features that may or may not be available on a given keyboard.

For full information about the spec please read the linked pdf above.

**TODO:** Add some examples for how to do simple kll things such as adding a new layout (workman?) or editing/adding layers.

> NOTE: Each keymap is done after the entire file is processed. This means that within the file the order
> of assignment does _not_ matter (if you assign the same thing twice, then yes the most recent one
> takes priority).

> NOTE: Don't use defaultMap.kll to change your layouts. This will work, but they will not be portable.

For information on how to use and combine kll files please see the [Keymaps page](Keymaps.md).
