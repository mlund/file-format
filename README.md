# file-format

![Build](https://img.shields.io/github/actions/workflow/status/mmalecot/file-format/ci.yml?branch=main)
[![Crates.io](https://img.shields.io/crates/v/file-format.svg)](https://crates.io/crates/file-format)
[![Docs](https://docs.rs/file-format/badge.svg)](https://docs.rs/file-format)
![Rust](https://img.shields.io/badge/rust-1.60+-blueviolet.svg?logo=rust)
![License](https://img.shields.io/badge/license-MIT%2FApache--2.0-blue.svg)

Crate for determining the file format of a given file or stream.

It provides a variety of functions for identifying a wide range of file formats, including ZIP,
Compound File Binary (CFB), Extensible Markup Language (XML) and much more.

It checks the signature of the file to determine its format and intelligently employs specific
readers when available for accurate identification. If the signature is not recognized, the crate
falls back to the default file format, which is Arbitrary Binary Data (BIN).

## Examples

Determines from a file:

```rust
use file_format::{FileFormat, Kind};

let format = FileFormat::from_file("fixtures/document/sample.pdf")?;
assert_eq!(format, FileFormat::PortableDocumentFormat);
assert_eq!(format.name(), "Portable Document Format");
assert_eq!(format.short_name(), Some("PDF"));
assert_eq!(format.media_type(), "application/pdf");
assert_eq!(format.extension(), "pdf");
assert_eq!(format.kind(), Kind::Document);
```

Determines from bytes:

```rust
use file_format::{FileFormat, Kind};

let format = FileFormat::from_bytes(&[0xFF, 0xD8, 0xFF]);
assert_eq!(format, FileFormat::JointPhotographicExpertsGroup);
assert_eq!(format.name(), "Joint Photographic Experts Group");
assert_eq!(format.short_name(), Some("JPEG"));
assert_eq!(format.media_type(), "image/jpeg");
assert_eq!(format.extension(), "jpg");
assert_eq!(format.kind(), Kind::Image);
```

## Usage

Add this to your `Cargo.toml`:

```toml
[dependencies]
file-format = "0.23"
```

## Crate features

All features below are disabled by default.

### Ecosystem features

- `serde` - Adds the ability to serialize and deserialize a `FileFormat` and `Kind` using serde.

### Reader features

These features enable the detection of file formats that require a specific reader for
identification.

- `reader` - Enables all reader features.
- `reader-asf` - Enables Advanced Systems Format (ASF) based file formats detection.
- `reader-cfb` - Enables Compound File Binary (CFB) based file formats detection.
- `reader-ebml` - Enables Extensible Binary Meta Language (EBML) based file formats detection.
- `reader-exe` - Enables MS-DOS Executable (EXE) based file formats detection.
- `reader-mp4` - Enables MPEG-4 Part 14 (MP4) based file formats detection.
- `reader-pdf` - Enables Portable Document Format (PDF) based file formats detection.
- `reader-rm` - Enables RealMedia (RM) based file formats detection.
- `reader-txt` - Enables Plain Text (TXT) detection when the file format is not recognized by its
  signature. Please note that this feature only detects files containing ASCII/UTF-8-encoded text.
- `reader-xml` - Enables Extensible Markup Language (XML) based file formats detection. Please note
  that these file formats may be detected without the feature in certain cases.
- `reader-zip` - Enables ZIP-based file formats detection.

## Supported file formats

### Application

- ActiveMime (MSO)
- Advanced Systems Format (ASF)
- Android Binary XML (AXML)
- Android Compiled Resources (ARSC)
- Apache Arrow Columnar (Arrow)
- Apache Avro Object Container (Avro)
- Apache Parquet (Parquet)
- Arbitrary Binary Data (BIN)
- BitTorrent File (Torrent)
- CD Audio (CDA)
- Compound File Binary (CFB)
- Digital Imaging and Communications in Medicine (DICOM)
- Empty
- Encapsulated PostScript (EPS)
- Extensible Binary Meta Language (EBML)
- Extensible Stylesheet Language Transformations (XSLT)
- Flexible Image Transport System (FITS)
- ICC Profile (ICC)
- Java KeyStore (JKS)
- MPEG-4 Part 14 (MP4)
- Mathematical Markup Language (MathML)
- Meta Information Encapsulation (MIE)
- Microsoft Compiled HTML Help (CHM)
- Microsoft Visual Studio Solution (SLN)
- MusicXML
- MusicXML Zipped (MXL)
- Ogg Multiplexed Media (OGX)
- PCAP Dump (PCAP)
- PCAP Next Generation Dump (PCAPNG)
- PEM Certificate Signing Request (PEM)
- PEM Private Key (PEM)
- PEM Public Key (PEM)
- PGP Message (PGP)
- PGP Private Key Block (PGP)
- PGP Public Key Block (PGP)
- PGP Signature (PGP)
- PGP Signed Message (PGP)
- Personal Storage Table (PST)
- PostScript (PS)
- RealMedia (RM)
- Simple Object Access Protocol (SOAP)
- Small Web Format (SWF)
- TASTy
- Tiled Map XML (TMX)
- Tiled Tileset XML (TSX)
- Windows Shortcut (LNK)
- XML Localization Interchange File Format (XLIFF)
- gettext Machine Object (MO)
- macOS Alias

### Archive

- 7-Zip (7Z)
- ALZ
- Advanced Compression Engine (ACE)
- Archived by Robert Jung (ARJ)
- Cabinet (CAB)
- Extensible Archive (XAR)
- LArc (LZS)
- LHA
- PMarc (PMA)
- Roshal Archive (RAR)
- SeqBox (SBX)
- Squashfs
- StuffIt (SIT)
- StuffIt X (SITX)
- Tape Archive (TAR)
- UNIX archiver (archiver)
- Windows Imaging Format (WIM)
- ZIP
- ZPAQ
- cpio
- zoo

### Audio

- Adaptive Multi-Rate (AMR)
- Adobe Flash Player Audio (F4A)
- Adobe Flash Player Audiobook (F4B)
- Advanced Audio Coding (AAC)
- Apple iTunes Audio (M4A)
- Apple iTunes Audiobook (M4B)
- Apple iTunes Protected Audio (M4P)
- Au
- Audio Codec 3 (AC3)
- Audio Interchange File Format (AIFF)
- Audio Visual Research (AVR)
- Creative Voice (VOC)
- FastTracker 2 Extended Module (XM)
- Free Lossless Audio Codec (FLAC)
- IFF 8-Bit Sampled Voice (8SVX)
- Impulse Tracker Module (IT)
- MPEG-1/2 Audio Layer 2 (MP2)
- MPEG-1/2 Audio Layer 3 (MP3)
- MPEG-4 Part 14 Audio (MP4)
- Matroska Audio (MKA)
- Monkey's Audio (APE)
- Musepack (MPC)
- Musical Instrument Digital Interface (MIDI)
- Ogg FLAC (OGA)
- Ogg Opus (Opus)
- Ogg Speex (Speex)
- Ogg Vorbis (Vorbis)
- Qualcomm PureVoice (QCP)
- Quite OK Audio (QOA)
- RealAudio (RA)
- Scream Tracker 3 Module (S3M)
- Sony DSD Stream File (DSF)
- SoundFont 2 (SF2)
- Ultimate Soundtracker Module (MOD)
- WavPack (WV)
- Waveform Audio (WAV)
- Windows Media Audio (WMA)

### Book

- Broad Band eBook (BBeB)
- Electronic Publication (EPUB)
- FictionBook (FB2)
- FictionBook Zipped (FBZ)
- Microsoft Reader (LIT)
- Mobipocket (MOBI)

### Certificate

- DER Certificate (DER)
- PEM Certificate (PEM)

### Compression

- BZip3 (BZ3)
- LZ4
- Lempel-Ziv Finite State Entropy (LZFSE)
- Lempel-Ziv-Markov chain algorithm (LZMA)
- Long Range ZIP (LRZIP)
- Snappy
- UNIX compress (compress)
- XZ
- Zstandard (zstd)
- bzip (BZ)
- bzip2 (BZ2)
- gzip (GZ)
- lzip (LZ)
- lzop (LZO)
- rzip (RZ)

### Database

- Microsoft Access 2007 Database (ACCDB)
- Microsoft Access Database (MDB)
- Microsoft Works Database (WDB)
- OpenDocument Database (ODB)
- SQLite 3

### Disk

- Amiga Disk File (ADF)
- Apple Disk Image (DMG)
- ISO 9660 (ISO)
- Microsoft Virtual Hard Disk (VHD)
- Microsoft Virtual Hard Disk 2 (VHDX)
- QEMU Copy On Write (QCOW)
- Virtual Machine Disk (VMDK)
- VirtualBox Virtual Disk Image (VDI)

### Document

- AbiWord (ABW)
- AbiWord Template (AWT)
- Adobe InDesign Document (INDD)
- Circuit Diagram Document (CDDX)
- InDesign Markup Language (IDML)
- Microsoft Excel Spreadsheet (XLS)
- Microsoft PowerPoint Presentation (PPT)
- Microsoft Project Plan (MPP)
- Microsoft Publisher Document (PUB)
- Microsoft Visio Drawing (VSD)
- Microsoft Word Document (DOC)
- Microsoft Works 6 Spreadsheet (XLR)
- Microsoft Works Spreadsheet (WKS)
- Microsoft Works Word Processor (WPS)
- Microsoft Write (WRI)
- Office Open XML Document (DOCX)
- Office Open XML Drawing (VSDX)
- Office Open XML Presentation (PPTX)
- Office Open XML Spreadsheet (XLSX)
- OpenDocument Formula (ODF)
- OpenDocument Formula Template (OTF)
- OpenDocument Graphics (ODG)
- OpenDocument Graphics Template (OTG)
- OpenDocument Presentation (ODP)
- OpenDocument Presentation Template (OTP)
- OpenDocument Spreadsheet (ODS)
- OpenDocument Spreadsheet Template (OTS)
- OpenDocument Text (ODT)
- OpenDocument Text Master (ODM)
- OpenDocument Text Master Template (OTM)
- OpenDocument Text Template (OTT)
- Portable Document Format (PDF)
- Rich Text Format (RTF)
- StarCalc (SDC)
- StarChart (SDS)
- StarDraw (SDA)
- StarImpress (SDD)
- StarMath (SMF)
- StarWriter (SDW)
- Sun XML Calc (SXC)
- Sun XML Calc Template (STC)
- Sun XML Draw (SXD)
- Sun XML Draw Template (STD)
- Sun XML Impress (SXI)
- Sun XML Impress Template (STI)
- Sun XML Math (SXM)
- Sun XML Writer (SXW)
- Sun XML Writer Global (SGW)
- Sun XML Writer Template (STW)
- WordPerfect Document (WPD)
- WordPerfect Graphics (WPG)
- WordPerfect Macro (WPM)
- draw.io (DRAWIO)

### Executable

- Common Object File Format (COFF)
- Dalvik Executable (DEX)
- Dynamic Link Library (DLL)
- Executable and Linkable Format (ELF)
- Java Class
- LLVM Bitcode (BC)
- Linear Executable (LE)
- Lua Bytecode
- MS-DOS Executable (EXE)
- Mach-O
- New Executable (NE)
- Nintendo Switch Executable (NSO)
- Optimized Dalvik Executable (DEY)
- Portable Executable (PE)
- WebAssembly Binary (Wasm)
- Xbox 360 Executable (XEX)
- Xbox Executable (XBE)

### Font

- Bitmap Font ASCII (FNT)
- Bitmap Font Binary (FNT)
- Embedded OpenType (EOT)
- OpenType (OTF)
- TrueType (TTF)
- Web Open Font Format (WOFF)
- Web Open Font Format 2 (WOFF2)

### Geospatial

- Flexible and Interoperable Data Transfer (FIT)
- GPS Exchange Format (GPX)
- Geography Markup Language (GML)
- Keyhole Markup Language (KML)
- Keyhole Markup Language Zipped (KMZ)
- Shapefile (SHP)
- Training Center XML (TCX)

### Image

- AV1 Image File Format (AVIF)
- AV1 Image File Format Sequence (AVIFS)
- Adaptable Scalable Texture Compression (ASTC)
- Adobe Illustrator Artwork (AI)
- Adobe Photoshop Document (PSD)
- Animated Portable Network Graphics (APNG)
- Apple Icon Image (ICNS)
- Better Portable Graphics (BPG)
- Canon Raw (CRW)
- Canon Raw 2 (CR2)
- Canon Raw 3 (CR3)
- Cineon (CIN)
- Digital Picture Exchange (DPX)
- DjVu
- Experimental Computing Facility (XCF)
- Free Lossless Image Format (FLIF)
- Fujifilm Raw (RAF)
- Graphics Interchange Format (GIF)
- High Efficiency Image Coding (HEIC)
- High Efficiency Image Coding Sequence (HEICS)
- High Efficiency Image File Format (HEIF)
- High Efficiency Image File Format Sequence (HEIFS)
- JPEG 2000 Codestream (J2C)
- JPEG 2000 Part 1 (JP2)
- JPEG 2000 Part 2 (JPX)
- JPEG 2000 Part 6 (JPM)
- JPEG Extended Range (JXR)
- JPEG Network Graphics (JNG)
- JPEG XL (JXL)
- JPEG-LS (JLS)
- Joint Photographic Experts Group (JPEG)
- Khronos Texture (KTX)
- Khronos Texture 2 (KTX2)
- Magick Image File Format (MIFF)
- Microsoft DirectDraw Surface (DDS)
- Multiple-image Network Graphics (MNG)
- Nikon Electronic File (NEF)
- Olympus Raw Format (ORF)
- OpenEXR (EXR)
- OpenRaster (ORA)
- Panasonic Raw (RW2)
- Picture Exchange (PCX)
- Portable Arbitrary Map (PAM)
- Portable BitMap (PBM)
- Portable FloatMap (PFM)
- Portable GrayMap (PGM)
- Portable Network Graphics (PNG)
- Portable PixMap (PPM)
- Quite OK Image (QOI)
- Radiance HDR (HDR)
- Scalable Vector Graphics (SVG)
- Silicon Graphics Image (SGI)
- Tag Image File Format (TIFF)
- WebP
- Windows Animated Cursor (ANI)
- Windows Bitmap (BMP)
- Windows Cursor (CUR)
- Windows Icon (ICO)
- Windows Metafile (WMF)
- X PixMap (XPM)
- farbfeld (FF)

### Model

- 3D Manufacturing Format (3MF)
- 3D Studio (3DS)
- 3D Studio Max (MAX)
- Additive Manufacturing Format (AMF)
- AutoCAD Drawing (DWG)
- Autodesk 123D (123DX)
- Autodesk Alias (WIRE)
- Autodesk Inventor Assembly (IAM)
- Autodesk Inventor Drawing (IDW)
- Autodesk Inventor Part (IPT)
- Autodesk Inventor Presentation (IPN)
- Blender (BLEND)
- Cinema 4D (C4D)
- Design Web Format (DWF)
- Design Web Format XPS (DWFX)
- Digital Asset Exchange (DAE)
- Drawing Exchange Format ASCII (DXF)
- Drawing Exchange Format Binary (DXF)
- Extensible 3D (X3D)
- Filmbox (FBX)
- Fusion 360 (F3D)
- GL Transmission Format Binary (GLB)
- Google Draco (Draco)
- Initial Graphics Exchange Specification (IGES)
- Inter-Quake Export (IQE)
- Inter-Quake Model (IQM)
- MagicaVoxel (VOX)
- Maya ASCII (MA)
- Maya Binary (MB)
- Model 3D ASCII (A3D)
- Model 3D Binary (M3D)
- Polygon ASCII (PLY)
- Polygon Binary (PLY)
- SketchUp (SKP)
- SolidWorks Assembly (SLDASM)
- SolidWorks Drawing (SLDDRW)
- SolidWorks Part (SLDPRT)
- SpaceClaim Document (SCDOC)
- Standard for the Exchange of Product model data (STEP)
- Stereolithography ASCII (STL)
- Universal 3D (U3D)
- Universal Scene Description ASCII (USDA)
- Universal Scene Description Binary (USDC)
- Universal Scene Description Zipped (USDZ)
- Virtual Reality Modeling Language (VRML)
- openNURBS (3DM)

### Package

- Adobe Integrated Runtime (AIR)
- Android Package (APK)
- Debian Binary Package (DEB)
- Enterprise Application Archive (EAR)
- Google Chrome Extension (CRX)
- Java Archive (JAR)
- Microsoft Software Installer (MSI)
- Microsoft Visual Studio Extension (VSIX)
- Nintendo Switch Package (NSP)
- Red Hat Package Manager (RPM)
- Web Application Archive (WAR)
- Windows App Package (APPX)
- XAP
- XPInstall (XPI)
- iOS App Store Package (IPA)

### Playlist

- Advanced Stream Redirector (ASX)
- MP3 URL (M3U)
- MPEG-DASH Manifest (MPD)
- SHOUTcast Playlist (PLS)
- Windows Media Playlist (WPL)
- XML Shareable Playlist Format (XSPF)

### ROM

- Atari 7800 ROM (A78)
- Game Boy Advance ROM (GBA)
- Game Boy Color ROM (GBC)
- Game Boy ROM (GB)
- Game Gear ROM (GG)
- Mega Drive ROM (MD)
- Neo Geo Pocket Color ROM (NGC)
- Neo Geo Pocket ROM (NGP)
- Nintendo 64 ROM (Z64)
- Nintendo DS ROM (NDS)
- Nintendo Entertainment System ROM (NES)
- Nintendo Switch ROM (XCI)
- Sega Master System ROM (SMS)

### Subtitle

- MPEG-4 Part 14 Subtitles (MP4)
- Matroska Subtitles (MKS)
- SubRip Text (SRT)
- Timed Text Markup Language (TTML)
- Universal Subtitle Format (USF)
- Web Video Text Tracks (WebVTT)

### Syndication

- Atom
- JSON Feed
- Really Simple Syndication (RSS)

### Text

- Clojure Script
- Extensible Markup Language (XML)
- HyperText Markup Language (HTML)
- LaTeX (TeX)
- Lua Script
- MS-DOS Batch (Batch)
- Perl Script
- Plain Text (TXT)
- Python Script
- Ruby Script
- Shell Script
- Tool Command Language Script (Tcl Script)
- WebAssembly Text (WAT)
- iCalendar (ICS)
- vCalendar (VCS)
- vCard (VCF)

### Video

- 3rd Generation Partnership Project (3GPP)
- 3rd Generation Partnership Project 2 (3GPP2)
- Actions Media Video (AMV)
- Adobe Flash Player Protected Video (F4P)
- Adobe Flash Player Video (F4V)
- Apple QuickTime (MOV)
- Apple iTunes Video (M4V)
- Audio Video Interleave (AVI)
- Autodesk Animator (FLI)
- Autodesk Animator Pro (FLC)
- BDAV MPEG-2 Transport Stream (M2TS)
- Flash Video (FLV)
- JPEG 2000 Part 3 (MJ2)
- MPEG-1/2 Video (MPG)
- MPEG-2 Transport Stream (TS)
- MPEG-4 Part 14 Video (MP4)
- MTV
- Material Exchange Format (MXF)
- Matroska 3D Video (MK3D)
- Matroska Video (MKV)
- Microsoft Digital Video Recording (DVR-MS)
- Ogg Media (OGM)
- Ogg Theora (Theora)
- RealVideo (RV)
- Silicon Graphics Movie (SGI)
- Sony Movie (MQV)
- WebM
- Windows Media Video (WMV)
- Windows Recorded TV Show (WTV)

## License

This project is licensed under either of:

* [Apache License, Version 2.0](LICENSE-APACHE)
* [MIT license](LICENSE-MIT)
