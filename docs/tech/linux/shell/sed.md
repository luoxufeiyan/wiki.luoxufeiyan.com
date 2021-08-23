# sed命令

## Substitute 替换

`s/` 开头

可用来提取字符

`sed -r "s/.*(COMP[0-9]{4}).html[^>]*>([^<]*)<.*/\1 \2/"`

数据如下：
```
r>
                              <td class="formBody" colspan="3">
                                 <table width="100%" cellspacing="0">
                                    <tr>
                                       <td width="20%" class="tableHeading">Code </td>
                                       <td width="50%" class="tableHeading">Course Title </td>
                                       <td width="30%" class="tableHeading">Units of Credit </td>
                                    </tr>
                                    <tr>
                                       <td class="rowSpacer" colspan="3"></td>
                                    </tr>
                                    <tr class="rowLowlight">
                                       <td class="data"><a href="COMP1000.html">COMP1000</a></td>
                                       <td class="data"><a href="COMP1000.html">Introduction to World Wide Web, Spreadsheets and Databases</a></td>
                                       <td class="data">6</td>
                                    </tr>
                                    <tr>
                                       <td class="rowSpacer" colspan="3"></td>
                                    </tr>
                                    <tr class="rowHighlight">
                                       <td class="data"><a href="COMP1010.html">COMP1010</a></td>
                                       <td class="data"><a href="COMP1010.html">The Art of Computing</a></td>
                                       <td class="data">6</td>
                                    </tr>
                                    <tr>
                                       <td class="rowSpacer" colspan="3"></td>
                                    </tr>
                                    <tr class="rowLowlight">
                                       <td class="data"><a href="COMP1511.html">COMP1511</a></td>
                                       <td class="data"><a href="COMP1511.html">Programming Fundamentals</a></td>
                                       <td class="data">6</td>
                                    </tr>
                                    <tr>
                                       <td class="rowSpacer" colspan="3"></td>
                                    </tr>
                                    <tr class="rowHighlight">
                                       <td class="data"><a href="COMP1521.html">COMP1521</a></td>
                                       <td class="data"><a href="COMP1521.html">Computer Systems Fundamentals</a></td>
                                       <td class="data">6</td>
                                    </tr>
                                    <tr>
                                       <td class="rowSpacer" colspan="3"></td>
                                    </tr>
                                    <tr class="rowLowlight">
                                       <td class="data"><a href="COMP1531.html">COMP1531</a></td>
                                       <td class="data"><a href="COMP1531.html">Software Engineering Fundamentals</a></td>
                                       <td class="data">6</td>
                                    </tr>
                                    <tr>
                                       <td class="rowSpacer" colspan="3"></td>
                                    </tr>
                                    <tr class="rowHighlight">
                                       <td class="data"><a href="COMP1911.html">COMP1911</a></td>
                                       <td class="data"><a href="COMP1911.html">Computing 1A</a></td>
                                       <td class="data">6</td>
                                    </tr>
                                    <tr>
                                       <td class="rowSpacer" colspan="3"></td>
                                    </tr>
                                    <tr class="rowLowlight">
                                       <td class="data"><a href="COMP2041.html">COMP2041</a></td>
                                       <td class="data"><a href="COMP2041.html">Software Construction: Techniques and Tools</a></td>
                                       <td class="data">6</td>
                                    </tr>
                                    <tr>
                                       <td class="rowSpacer" colspan="3"></td>
                                    </tr>
```


替换后： COMP1000  Introduction to World Wide Web, Spreadsheets and Databases