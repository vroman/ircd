# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Changed
- if DBPATH doesn't exists shows an error message and dies.
- Database files are created on DBPATH at ircd execution if they doesn't exists. 

### Removed
- Support for the following operating systems has been removed: AIX, BSD/OS, DYNIX, FreeBSD,
  HPUX, NetBSD, OSF, RISC/os, SGI, SunOS (Solaris)
