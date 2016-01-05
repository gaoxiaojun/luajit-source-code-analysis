# LuaJIT IR


## IR一些特点

## IR指令格式
<div>
<table border="1" align="center">
  <tr align="center">
    <td colspan="8">IR Format</td>
  </tr>
  <tr align="center">
    <td colspan="2" widtd="25%">16bit</td>
    <td colspan="2" widtd="25%">16bit</td>
    <td>8bit</td>
    <td>8bit</td>
    <td>8bit</td>
    <td>8bit</td>
  </tr>
  <tr border="1" align="center">
    <td colspan="2">op1</td>
    <td colspan="2">op2</td>
    <td>t</td>
    <td>o</td>
    <td>r</td>
    <td>s</td>
  </tr>
  <tr align="center">
    <td colspan="4">op12/i/gco/ptr</td>
    <td colspan="2">ot</td>
    <td colspan="2">prev</td>
  </tr>
</table>
</div>

### 指令字段的含义
|字段 |含义                        |
|:---:|:--------------------------:| 
|ot   |   IR opcode and type       |
|prev | Previous ins in same chain |
|t    |    IR type                 |
|o    |    IR opcode               |
|r    |    Register allocation     |
|s    |    Spill slot allocation   |
|i    | 32 bit signed integer literal|
|gco  | GCObj constant |
|ptr  | Pointer constant|

## IR指令详解
### Guarded Assertions
|op|left|right|description|
|--|:--:|:--:|--|
|LT|left|right| left < right (signed)|
|GE|left|right| left >= right (signed)|
|LE|left|right| left <= right (signed)|
|GT|left|right| left > right (signed)|
|ULT|left|right| left < right (unsigned/unordered)|
|UGE|left|right| left >= right (unsigned/unordered)|
|ULE|left|right| left <= right (unsigned/unordered)|
|UGT|left|right| left > right (unsigned/unordered)|
|EQ|left|right| left = right|
|NE|left|right| left != right |
|ABC|bound|index| Array Bounds Check: bound > index (unsigned)|
|RETF|proto|pc| Return to lower frame: check target PC, shift base|

### Micellaneous Ops
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|NOP||
|BASE||
|PVAL||
|GCSTEP||
|HIOP||
|LOOP||
|USE||
|PHI||
|RENAME||
|PROF||

### Constants
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|KPRI||
|KINT||
|KGC||
|KPTR||
|KKPTR||
|KNULL||
|KNUM||
|KINT64||
|KSLOT||

### Bit Ops
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|BNOT||
|BSWAP||
|BAND||
|BOR||
|BXOR||
|BSHL||
|BSHR||
|BSAR||
|BROL||
|BROR||

### Arithmetic Ops
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|ADD||
|SUB||
|MUL||
|DIV||
|MOD||
|POW||
|NEG||
|ABS||
|ATAN2||
|LDEXP||
|MIN||
|MAX||
|FPMATH||
|ADDOV||
|SUBOV||
|MULOV||

### Memory References
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|AREF||
|HREFK||
|HREF||
|NEWREF||
|UREFO||
|UREFC||
|FREF||
|STRREF||
|LREF||

### Loads and Stores
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|ALOAD||
|HLOAD||
|ULOAD||
|FLOAD||
|XLOAD||
|SLOAD||
|VLOAD||
|ASTORE||
|HSTORE||
|USTORE||
|FSTORE||
|XSTORE||

### Allocations
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|SNEW||
|XSNEW||
|TNEW||
|TDUP||
|CNEW||
|CNEWI||

### Buffer
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|BUFHDR||
|BUFPUT||
|BUFSTR||

### Barriers
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|TBAR||
|OBAR||
|XBAR||

### Type Conversions
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|CONV||
|TOBIT||
|TOSTR||
|STRTO||

### Calls
|OP|Left|Right|Description|
|--|:--:|:--:|--|
|CALLN||
|CALLA||
|CALLL||
|CALLS||
|CALLXS||
|CARG||

## IR的一些数据结构
IRRef1 uint16_t IRRef2 uint32_t
IRRef 代表在指令数组里的位置

<table>
    <tr align="center">
        <td colspan="4">Tagged IR References(32bit)</td>
    </tr>
    <tr align="center">
        <td widtd="25%">irt</td>
        <td widtd="25%">flags</td>
        <td colspan=2 widtd="50%">ref</td>
    </tr>
</table>
