# Gradle
## Introduction
This is the docs for gradle, not just for this project but detailing what each file does to enable the recreation of all parts of the project. 
Gradle is the dependency manager for this project. Android studio has its own version of gradle so you do not need to install it on your system.

## Root
In the root of the project, there are some required files.

## App level
### build.gradle (app level)
#### plugins
The plugin `id("com.android.application")` enables the android build pipeline. This plugin is the defining plugin for android applications, compiling resources into the generated R class, merging AndroidManifest.xml, converts bytecode into DEX (the android runtime format), and similar supporting features within the android build pipeline.

The plugin `id("org.jetbrains.kotlin.android")` Applies the Kotlin tooling for Android modules, including enabling .kt sources as part of the Android build. 

#### minify and proguard