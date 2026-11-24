# ATLAS — Release, Packaging and Code-Signing Plan

**Status:** Planning document. No signing provider, certificate, store listing or final packaging workflow has been selected or secured yet.

## Release targets and timing

- **Initial platforms:** Windows and Linux.
- **ATLAS Core:** target release in **mid-March 2027**.
- **ATLAS Pro:** development is planned to begin in **late March 2027**, building on the Core foundation.

These are project targets, not guaranteed dates. Release readiness depends on working builds, installation tests, security checks and clear documentation.

## Distribution goals

- Publish source code and release notes through the ATLAS GitHub repository.
- Provide ready-to-install builds through GitHub Releases so users and evaluators do not need to compile the project themselves.
- Keep release artifacts, checksums and version information easy to verify.
- Make the installation experience clear about publisher identity, platform requirements and any remaining trust warnings.

## Windows: signing concern

Unsigned Windows installers can trigger Microsoft Defender SmartScreen or other reputation-based warnings. This creates friction and can make a legitimate student-built open-source application look unfamiliar or untrusted. Code signing helps establish publisher identity and artifact integrity, but it does **not** guarantee that SmartScreen warnings disappear immediately; reputation and distribution context can still matter.

The preferred outcome is to publish a properly signed Windows installer for the public Core release. This is a goal, not yet a confirmed capability.

### Options to investigate

1. **SignPath Foundation:** investigate whether ATLAS and its maintainers meet the programme's current eligibility, licensing, repository, release and verification requirements. Do not assume acceptance or free signing until eligibility is confirmed directly.
2. **Microsoft Store:** investigate Store distribution and its signing/install experience as a possible complementary route. Store distribution is not automatically equivalent to signing a separate installer distributed through GitHub Releases.
3. **Other student/open-source programmes or certificate options:** ask experienced student developers and Hack Club community members about current programmes, eligibility and practical experience. Verify terms and availability before relying on any option.
4. **Paid code-signing certificate:** keep this as a fallback to research with a parent/guardian if an appropriate free route is unavailable. Do not purchase or enter into a certificate agreement without the required adult involvement.

### Community research

In February 2027, ask the Hack Club Slack community how student developers handle Windows code signing and distribution for open-source desktop apps. Ask specifically about free signing programmes, eligibility, SmartScreen experience, and whether they distribute signed installers, Store builds or another format.

Do not publish private keys, certificate files, tokens or account credentials in the repository or CI logs. Any eventual signing workflow must protect signing material and use appropriately restricted access.

### If signing is unavailable for Core

Do not conceal the unsigned status or imply that a build is signed. Decide before release whether to:
- publish an explicitly labelled unsigned build with clear installation and trust-warning guidance; or
- delay the public Windows installer while continuing to provide source code and tested builds through an appropriate channel.

The decision should be based on safety, user trust and release readiness—not on bypassing operating-system security warnings.

## Linux packaging

Investigate practical formats for the target distributions, initially considering:
- **AppImage** for a portable application bundle.
- **DEB** for Debian/Ubuntu-based distributions.

Add other formats only when there is a clear user need and the project can test and maintain them. Publish SHA-256 checksums and, where practical, signed release metadata. Linux package signing and repository trust are different from Windows Authenticode signing; document the actual verification method used.

## Release pipeline

The intended pipeline should:
- build Windows and Linux artifacts in reproducible, documented CI workflows where practical;
- run automated checks and platform-specific smoke tests;
- attach versioned release notes and checksums;
- keep development/pre-release builds distinct from stable releases;
- record exactly which source revision produced each published artifact;
- never claim a platform or artifact is verified unless it has been tested.

Possible initial artifact names (subject to the final packaging toolchain):
- Windows: `ATLAS-Setup-x64.exe` and optionally `ATLAS-x64-Portable.zip`.
- Linux: `ATLAS-x86_64.AppImage` and `ATLAS-amd64.deb`.

## Decisions still open

- Signing provider and confirmed eligibility.
- Whether Core's Windows installer can be signed before mid-March 2027.
- Final Windows installer and update strategy.
- Exact Linux packaging formats and supported distribution baseline.
- Whether a Microsoft Store listing is worthwhile.
- Final licence choice; this must be decided before relying on any programme whose eligibility depends on the project's licence.

## Release checklist

- [ ] Confirm the open-source licence and publish the licence file.
- [ ] Confirm Windows and Linux build targets and minimum OS versions.
- [ ] Select and validate packaging tools.
- [ ] Investigate signing programmes and verify eligibility directly.
- [ ] Ask the Hack Club community for student developer experiences in February 2027.
- [ ] Test clean installation, launch, upgrade and uninstall on supported systems.
- [ ] Verify checksums and release provenance.
- [ ] Clearly disclose whether each Windows artifact is signed.
- [ ] Publish release notes, known issues and installation instructions.
