# LuaJIT IR


## IR一些特点

## IR指令格式

<table border="1" align="center">
  <tr align="center">
    <th colspan="2" width="25%">16bit</th>
    <th colspan="2" width="25%">16bit</th>
    <th>8bit</th>
    <th>8bit</th>
    <th>8bit</th>
    <th>8bit</th>
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
    <td colspan="4">op12/i/gco </td>
    <td colspan="2">ot</td>
    <td colspan="2">prev</td>
  </tr>
</table>


 prev is only valid prior to register allocation and tden reused for r + s.

## IR指令详解
