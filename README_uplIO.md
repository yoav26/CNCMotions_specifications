## uplIO

digital and analog I/O helpers, scoped per axis through `AChooseAxis[AProgThread]`.

### Naming convention

Functions follow **`uplIO` + controller keyword + action**:

| Pattern | Example |
|---------|---------|
| `uplIO` + `DInPort` + `Read` | `uplIODInPortRead` |
| `uplIO` + `DOutPort` + `Write` | `uplIODOutPortWrite` |
| `uplIO` + `DInMode` + `Set` | `uplIODInModeSet` |
| `uplIO` + `DOutSelect` + `Read` | `uplIODOutSelectRead` |

### Controller digital I/O model

| Keyword | Type | Index / bit rule |
|---------|------|------------------|
| `DInPort` | 32-bit | bit *n* → input #(*n*+1); input #1 = bit 0 |
| `DInLog` | 32-bit | same bit mapping as `DInPort` |
| `DInMode[]` | 32 × | array index → input # (**1-based**) |
| `DOutPort` | 32-bit | bit *n* → output #(*n*+1); output #1 = bit 0 |
| `DOutLog` | 32-bit | same bit mapping as `DOutPort` |
| `DOutMode[]` | 32 × | array index → output # (**1-based**) |
| `DOutSelect[]` | 16 × | array index → output # (**1-based**) |
| `DOutType` | 32-bit | per-bit: `DOUTTYPE_SINK` (0) / `DOUTTYPE_SOURCE` (1) |

UPL access: `PDInPort`, `PDInLog`, `PDInMode[]`, `PDOutPort`, `PDOutLog`, `PDOutMode[]`, `PDOutSelect[]`, `PDOutType` after axis selection.


### Integration example

```
uplIODOutModeSet(A_AXIS, 1, DOUTMODE_USER_OUTPUT)
uplIODOutPortWrite(A_AXIS, 0)
uplIODOutPortSetBits(A_AXIS, DOUTPORT_DOUT1_SET)
AWaitTime, 500
uplIODOutPortClearBits(A_AXIS, DOUTPORT_DOUT1_CLEAR)

l:din  = uplIODInPortRead(A_AXIS)
l:dlog = uplIODInLogRead(A_AXIS)
```

### Digital functions

| Function | Returns | Maps to |
|----------|---------|---------|
| `uplIODInPortRead(lAxis_)` | `l` | `PDInPort` |
| `uplIODInLogRead(lAxis_)` | `l` | `PDInLog` |
| `uplIODInModeSet(lAxis_, InputIndex_, Mode_)` | — | `PDInMode[InputIndex_]` |
| `uplIODOutPortRead(lAxis_)` | `l` | `PDOutPort` |
| `uplIODOutPortWrite(lAxis_, value_)` | — | `PDOutPort` |
| `uplIODOutPortSetBits(lAxis_, BitMask_)` | — | `PDOutPort \|= mask` |
| `uplIODOutPortClearBits(lAxis_, BitMask_)` | — | `PDOutPort &= mask` |
| `uplIODOutPortToggleBits(lAxis_, BitMask_)` | — | `PDOutPort ^= mask` |
| `uplIODOutLogRead(lAxis_)` | `l` | `PDOutLog` |
| `uplIODOutModeSet(lAxis_, OutputIndex_, Mode_)` | — | `PDOutMode[OutputIndex_]` |
| `uplIODOutSelectRead(lAxis_, SelectIndex_)` | `l` | `PDOutSelect[SelectIndex_]` |
| `uplIODOutSelectWrite(lAxis_, SelectIndex_, value_)` | — | `PDOutSelect[SelectIndex_]` |
| `uplIODOutTypeRead(lAxis_)` | `l` | `PDOutType` |
| `uplIODOutTypeWrite(lAxis_, value_)` | — | `PDOutType` |

Port bit masks: `DINPORT_DINn_BIT`, `DOUTPORT_DOUTn_BIT` / `_SET` / `_CLEAR` (n = 1..32).  
Mode constants: `DINMODE_*`, `DOUTMODE_*` in `uphGeneralConstants.puh2`.

### Analog functions (unchanged scope)

| Function | Returns | Maps to |
|----------|---------|---------|
| `uplIOAInModeSet(lAxis_, InputIndex_, Mode_)` | — | `PAInMode[InputIndex_]` |
| `uplIOAInPortRead(lAxis_, Index_)` | `f` | `PAInPort[Index_]`; **`Index_` > 0** |

### Constants (`uphGeneralConstants.puh2`)

- `DINMODE_*`, `DOUTMODE_*`, `DOUTTYPE_SINK` / `DOUTTYPE_SOURCE`
- `IO_DIN_COUNT` (32), `IO_DOUT_COUNT` (32), `IO_DOUT_SELECT_COUNT` (16)
- `DINPORT_DINn_BIT`, `DOUTPORT_DOUTn_BIT` / `_SET` / `_CLEAR`
