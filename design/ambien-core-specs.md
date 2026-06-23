# `ambien-core` Specs

## Requirements
- [ ] Ability to be used as a library
    - There will be `ambien-cli` & `ambien-gui` to interface with the core library.
    - The `ambien-core` will have a test project for development.
- [ ] Gradle integration
- [ ] Strip `ambien-anno` annotations
- [ ] Write original files unless modified
    - The class transform method should return a boolean for if the class was modified or not.
- [ ] Support for `.jar`, `.class` & `.apk` input files
- [ ] Check for missing settings
    - Check for entire transformers missing & transformer specific settings missing.
    - If a setting is missing, warn & create a new settings file with the missing settings; append `-{COMMIT_HASH}` to name.
    - If a required setting (input/output string) is missing, throw an exception.

### Transformers

##### Transformer class
- [ ] Pretty name (for gui & logging) & separate settings name
- [ ] Description (for gui & help command)
- [ ] Tags array
    - control-flow
    - encryption
    - exploit
    - packaging
    - miscellaneous
- [ ] Transformer version string ("1.0", "1.1", etc.)
- [ ] Stability
    - STABLE ~ Very unlikely to break anything
    - UNSTABLE ~ Likely to break something in complex edge cases
    - EXPERIMENTAL ~ Still in development, not the final version of the transformer
- [ ] Ordinal
    - LOWEST ~ Transformer MUST be applied last (only one transformer can have this)
    - LOW ~ Transformer is applied last
    - STANDARD ~ Doesn't matter when the transformer is applied
    - HIGH ~ Transformer is applied first
- [ ] Supported files array 
    - JAR_FILES for transformers that require a .jar input file
    - CLASS_FILES for transformers that only require a class file as input
- [ ] Enabled by default & always enabled

##### Shrink transformers
- [ ] Hardcoded password & api key check
- [ ] Unused variables & methods remover
    - Removes unused class variables & variables from methods

##### Obfuscation transformers
- [ ] String encryption
    - [ ] Strength/Encryption algorithm option
    - [ ] Decryption time
        - When the decryption will occur.
        - [ ] Class initialization 
            - Decrypts string during class initialization & stores in an array.
        - [ ] During execution
            - Regular string encryption, decrypts strings when needed.
- [ ] Operator replacer
    - Replaces operators with `x` different operators to produce the same output
    - [ ] Number of replacement operators
- [ ] Literal number encryption
    - [ ] Complex operators
        - Replaces operators with a more complex operations
        - Example: `2+2` would become `12 % 8`
- [ ] Class encryption
    - Encrypts classes & adds a custom class loader that decrypts them at runtime.
- [ ] Watermark
    - Adds obfuscation watermark to exported file, always enabled.

##### Miscellaneous
- [ ] Ability to write custom transformers using JavaScript
    - This feature may be scrapped.

## Dependencies
- [lombok](https://projectlombok.org/)
- [gson](https://github.com/google/gson)
- [asm](https://asm.ow2.io/)

## Design
The current design can be viewed [here](ambien-core-design.mmd). If you don't know how to view `.mmd` (Mermaid) files check the [design readme](README.md).