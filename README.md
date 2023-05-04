Download Link: https://assignmentchef.com/product/solved-csci-621-programming-languages-programming-assignment-3-a-non-recursive-predictive-parser
<br>
Design and implement a Non-recursive Predictive Parser (NPP) for the following grammar:

&lt;elist&gt; → &lt;elist&gt; , &lt;e&gt; | &lt;e&gt;

&lt;e&gt; → &lt;n&gt; ^ &lt;e&gt; | &lt;n&gt;

&lt;n&gt; → &lt;n&gt; &lt;d&gt; | &lt;d&gt;

&lt;d&gt; → 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9




Where ^ is an exponentiation operator (associate to right). This grammar generates statements of the form 2^2^3, 15, 20^2 for which the parser outputs 256 15 400.




<strong>Solution: </strong>

In order to implement this NPP, a parse table must be constructed by using first sets and follow sets.




The parse table for this parser is shown as follows:




<table width="664">

 <tbody>

  <tr>

   <td width="61"> </td>

   <td width="139"><strong>d</strong></td>

   <td width="83"> </td>

   <td width="93"><strong>^</strong></td>

   <td width="168"><strong>, </strong></td>

   <td width="120"><strong>$</strong></td>

  </tr>

  <tr>

   <td width="61"><strong>elist </strong></td>

   <td width="139"><strong>elist</strong>→<strong> e  elist’</strong></td>

   <td width="83"> </td>

   <td width="93"> </td>

   <td width="168"> </td>

   <td width="120"> </td>

  </tr>

  <tr>

   <td width="61"><strong>elist’</strong></td>

   <td width="139"> </td>

   <td width="83"> </td>

   <td width="93"> </td>

   <td width="168"><strong>elist’ </strong>→<strong> ,  elist</strong></td>

   <td width="120"><strong>elist’ </strong>→ </td>

  </tr>

  <tr>

   <td width="61"><strong>e</strong></td>

   <td width="139">e → n e’</td>

   <td width="83"> </td>

   <td width="93"> </td>

   <td width="168"> </td>

   <td width="120"> </td>

  </tr>

  <tr>

   <td width="61"><strong>e’</strong></td>

   <td width="139"> </td>

   <td width="83">e<sup>’</sup>→ ^ e</td>

   <td width="93"> </td>

   <td width="168">e<sup>’</sup> → </td>

   <td width="120">e<sup>’</sup> → </td>

  </tr>

  <tr>

   <td width="61"><strong>n</strong></td>

   <td width="139">n → d n’</td>

   <td width="83"> </td>

   <td width="93"> </td>

   <td width="168"> </td>

   <td width="120"> </td>

  </tr>

  <tr>

   <td width="61"><strong>n’</strong></td>

   <td width="139">n’ →n</td>

   <td width="83">n’ → </td>

   <td width="93"> </td>

   <td width="168">n’ → </td>

   <td width="120">n’ → </td>

  </tr>

 </tbody>

</table>

1







The Non-recursive Predictive Parsing Algorithm is:




Let T$ be the input string followed by a $.

Set ip to point to the first symbol of T$. Repeat

Let X be the top of stack symbol.

Let <strong>a</strong> be the symbol pointed to by ip.

IF X is a terminal or $ THEN

IF X== <strong>a</strong> THEN

Pop X from the stack and advance ip

ELSE error()

ELSE IF M[X,<strong>a</strong>] == X→Y<sub>1</sub>Y<sub>2</sub>…Y<sub>k </sub> THEN

BEGIN

pop X from the stack

push Y<sub>k</sub>,Y<sub>k-1</sub>,…,Y<sub>1 </sub>onto to the stack with Y<sub>1</sub> on the top

output X→Y<sub>1</sub>Y<sub>2</sub>…Y<sub>k </sub>

END

ELSE error()

UNTIL X == $




2


