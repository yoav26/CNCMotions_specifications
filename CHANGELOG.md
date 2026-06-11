# Changelog

## 1.6.0

### No behavioral change

- Expanded `README_uplIO.md` with controller digital I/O keyword table.

### Behavioral change

- **uplIO** digital I/O coverage (additive):
  - `uplIODInLogRead`, `uplIODOutLogRead`
  - `uplIODOutSelectRead`, `uplIODOutSelectWrite`
  - `uplIODOutTypeRead`, `uplIODOutTypeWrite`
- **Constants** (`uphGeneralConstants.puh2`):
  - `DOUT_*` mode values renamed to `DOUTMODE_*` (breaking)
  - Added `DOUTTYPE_SINK` / `DOUTTYPE_SOURCE`, `IO_DIN_COUNT`, `IO_DOUT_COUNT`, `IO_DOUT_SELECT_COUNT`
  - Extended `DINPORT_DINn_BIT` and `DOUTPORT_DOUTn_BIT` / `_SET` / `_CLEAR` to n = 1..32

---

## 1.5.0

### No behavioral change

- None.

### Behavioral change

- **uplIO** function rename to `uplIO<Keyword><Action>` convention (breaking):
  - `uplIOReadDInPort` → `uplIODInPortRead`
  - `uplIOReadDOutPort` → `uplIODOutPortRead`
  - `uplIOWriteDOutPort` → `uplIODOutPortWrite`
  - `uplIOSetDOutBits` → `uplIODOutPortSetBits`
  - `uplIOClearDOutBits` → `uplIODOutPortClearBits`
  - `uplIOToggleDOutBits` → `uplIODOutPortToggleBits`
  - `uplIOSetDInMode` → `uplIODInModeSet`
  - `uplIOSetDOutMode` → `uplIODOutModeSet`
  - `uplIOSetAInMode` → `uplIOAInModeSet`
  - `uplIOReadAIn` → `uplIOAInPortRead`

---

## 1.4.0

### No behavioral change

- Updated `README_uplIO.md` and `LIBRARY_CONVENTIONS.md` to reflect narrowed `uplIO` scope.

### Behavioral change

- Removed `uplIOWaitDIn` and `uplIOCheckDInTrigger` from `uplIO` (program-level DIn polling did not belong in the I/O module).
- Removed `TRIG_*` from `uphGeneralConstants.puh2` and `IO_DIN_MASK_ALL` from `uplIO.puh2` (only used by the removed wait helpers).
- Use `uplCNCWaitInput` for in-motion input wait; use `uplIODInPortRead` or dedicated `DInMode` configuration for idle/program logic.

---

## 1.3.0

### No behavioral change

- Added `uplIO` module (`uplIO.puh2`, `uplIO.pup2`) for immediate per-axis digital/analog I/O and mode configuration.
- Added `README_uplIO.md` and updated `LIBRARY_CONVENTIONS.md` / project file list.
- Existing module APIs (`uplMotion`, `uplUtility`, `uplCNC`) unchanged.

### Behavioral change

- None for previously published APIs in this release tag.

---

## 1.2.0

### No behavioral change

- Added `LIBRARY_CONVENTIONS.md` as a single-source conventions spec.
- Normalized terminology, comment wording, and naming consistency across UPL files and CNC docs.
- Aligned CNC documentation to match actual function names and parameter push order.
- Added module documentation artifacts:
  - `README_uplCNC.md`
  - `README_uplMotions.md`
  - `README_uplUtility.md`
  - `README_Integration_Example.md`
- Added release-readiness structure and examples for packaging/review.

### Behavioral change

- None in this release tag.

---

## Versioning Notes

- Library modules are aligned to `1.2.0` for this conventions/documentation release.
- Future releases must classify every item under either:
  - `No behavioral change`
  - `Behavioral change`
