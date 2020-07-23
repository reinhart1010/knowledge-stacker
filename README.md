# "Knowledge" Card Stacking Algorithm
## All about this project
This project is initially started to design an effective algorithm to align and stack [Cards (User Interface)](https://material.io/components/cards) on a fixed, three-column layout. This design is similar to the home screen of Windows 10 Mobile where the [App Tiles](https://docs.microsoft.com/en-us/windows/uwp/design/shell/tiles-and-notifications/creating-tiles) can be customized by size and content.

The goal of this project is to recreate the three-column layout used in ["Knowledge" microsite](https://binus.ac.id/knowledges) and an account dashboard used in [BINUS University](https://binus.ac.id). Note that these cards are statically generated (the amount and content of each card stays the same over time), and without an efficient algorithm, it will be difficult to generate a similar layout with random cards and spanning content.

![image](https://user-images.githubusercontent.com/17312341/88274622-31f72600-cd06-11ea-8fd4-217a74a7374a.png)
![image](https://user-images.githubusercontent.com/17312341/88274510-070cd200-cd06-11ea-8443-7fa05d3f0bf0.png)

## Card Specification
On desktop, each card is defined a fixed width and height. For "regular" (1x1) cards, this means that its height is the same as its (column) width, which is defined as a third of the overall page width, with several adjustments on margin and padding. Spanning cards (2x1, 3x1, 2x2, etc.) will take up more dimensions, but this will create gaps on the overall layout when there are no smaller cards that can complement them.

This is why each card should be able to squeeze into 1x1 layout, while maintaining flexibility on larger sizes. In this project, these cards will be able to define their own `compatibledimensions` to be calulated by the algorithm. Futhermore, interactive cards will be able to have different appearances on different sizes. For example, a video card (e.g. YouTube) will show an embedded preview on a 2x1 layout, while on 1x1 it will show a thumbnail with link to respective websites. Note that the details of these interactive cards are outside the scope of this project.

These things will be significantly different on tablet and mobile. Depending on the device's width, smaller tablets will get a two-column layout and mobile users will instead get a single column. These cards will have a flexible height and do not span across columns, similar to the ones shown on [Android Slices](https://developer.android.com/guide/slices), iOS' legacy "Today View" widgets (iOS 8-13), and the Google App (formerly known as Google Now).

## Algorithm Implementation
In order to implement algorithm prototypes easily, we have decided to use the C programming language with simplified input/output model. Unlike the rich, "Knowledge" view above, the program will output a layout similar to this.
```
AAF
AAG
BBB
ECC
EDD
HH
```
This output refers to the position of the Card ID (represented as a single `char`) which have been arranged by the algorithm. Using the example above, we can tell that `F` is placed as a 1x1 card, `E` as 1x2, `H` as 2x1, `A` as 2x2, etc.

The program input will be a JSON buffer which is read from `stdin`. A bunch of sample JSON files are provided for testing purposes. To read from a file, use the default shell's arrow functions, for example:
```
testdata.json > stacker.exe # Windows
testdata.json > stacker     # macOS, Linux, and other POSIX-compliant operating systems
```
This program will depend on [cJSON](https://github.com/DaveGamble/cJSON) library (included) for JSON parsing.

## Testing
It is easy to write tests for this algorithm, even when using C. However, the test results may differ between changes and commits. It is recommended to report issues ONLY where there are errors and gaps (shown as a whitespace " " character) shown on the program output, rather than output differences within repeated test attempts. The algorithm IS designed to randomly stack cards, in order to provide a unique output due to User Experience reasons.
