This is my own attempt at creating a good and solid specification for [Romantic Versioning](https://github.com/romversioning/romver).



## Definition

Romantic Versioning (or RomVer) is inspired by [SemVer](https://semver.org/), but is meant to better fit the way that humans naturally percieve version changes. In short, RemVer is defined as `vHUMAN.MAJOR.MINOR`, where HUMAN is incremented when there is a large conceptual change, MAJOR is incremented when there are breaking changes, and MINOR is incremented when non-breaking changes are made.

<br>

## Why was this made?

This was made to fix the confusion that SemVer often creates regarding MAJOR changes. When a project releases a v2.0, people don't automatically think of it as a simple breaking change as they should, they think of it as being an extremely big deal. And conversely, when a project released a v54.0, people don't automatically think of it as a simple breaking change as they should, they think of it as another small tedious step that isn't noteworthy.

<br>

## Why should this be used?

- 1: It is very intuitive for everyone involved (users, maintainers, etc)
- 2: It is compatible with systems that expect SemVer
- 3: It is possibly the least likely format to cause confusion and wrongful assumptions

<br>
<br>
<br>

## Formal specification (as a list of details):

<br>

1: &nbsp; If a string in this specification is inside single quotes, it is being defined for later use.

2: &nbsp; The 'RomVer Format' is defined as "vHUMAN.MAJOR.MINOR", where "HUMAN", "MAJOR", and "MINOR" are each placeholders for positive integers.

3: &nbsp; If applicable, the RomVer Format must be extended in the following way(s):

&nbsp; &nbsp; &nbsp; 3.1: &nbsp; If a release is a preview for a 'Planned Future Release', its Version must be the expected Version of the Planned Future Release concatenated with "-pre" and a number which is incremented for each preview release for the Planned Future Release and starts at 1.

4: &nbsp; A 'Version' is defined as an ASCII string that follows the RomVer Format, even if the leading "v" is omitted.

5: &nbsp; If a 'Project' wishes to follow the RomVer standard, it must follow every following rule.

6: &nbsp; Each release of the Project must have exactly one Version attached.

7: &nbsp; The contents (counted recursively) of each release of the Project must remain strictly unchanged in every possible manner once released, as much as relevant systems will allow. If the contents of a release require change, the change must be issued as a new release.

8: &nbsp; The Version for the first release of the Project must be "v0.1.0" if the project is considered unfit for stable use, or "v1.0.0" if it is considered fit for stable use.

9: &nbsp; Each Version of each release (or the New Release) of the Project must be based off the Version of whichever release the New Release was based on (or the Old Release), and must differ according to these rules:

&nbsp; &nbsp; &nbsp; 9.1: &nbsp; If the New Release is considered significantly different in a conceptual sense compared to the Old Release, or if the New Release is considered fit for stable use and the Old Release is not, the HUMAN segment of the Version must be incremented and the MAJOR and MINOR segments must be reset to 0.

&nbsp; &nbsp; &nbsp; 9.2: &nbsp; Otherwise, if users might encounter breaking changes compared to the Old Release, the MAJOR segment of the Version must be incremented and the MINOR segment must be reset to 0, but the HUMAN segment must stay the same.

&nbsp; &nbsp; &nbsp; 9.3: &nbsp; Otherwise, the MINOR segment must be incremented, but the HUMAN and MAJOR segments must stay the same.

10: &nbsp; A Version (VA) is considered numerically greater than another (VB) if the HUMAN segment of VA is greater than VB's, or if the HUMAN segments are the same then the MAJOR segments are compared, or if the MAJOR segments are the same then the MINOR segments are compared, or if the MINOR segments are the same then the pre-release segments (if available, else "-pre0") are compared, or if the pre-release segments are the same then VA is equal to VB.

<br>

## Notes

- Concepts like release alphas and betas are not recognized by this format
- There are many times when you can and should have releases that do not strictly increase the version number compared to the last release (such as fixes for versions of the project which are older but still supported)
