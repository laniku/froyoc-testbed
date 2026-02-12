## Froyocomb Testbed


> [!CAUTION]
> These builds are not to be documented until they reach completion and the manifest and patches are moved into their appropriate folder. Upon completion, they will be upstreamed into the Froyocomb project.

The build that is currently being worked on in this repo is: **MIY71B**

#### Notes:
- Breakpad has a bad example project which must be removed from the source tree.
`rm -rf external/google-breakpad/Android/sample_app/`
- Address sanitation is totally messed up here due to tons of mismatches with upstream Clang. Patches for various Android.mk files will be included.
- This build will ONLY work on arm32 for the time being.
- IFDEF for various libc functions go missing and will be correctly stubbed. Instructions will come later.

> [!TIP]
> Builds like these create a lot of artifacts. If you run into problems related to artifacts after running make clean, run make clobber instead,
