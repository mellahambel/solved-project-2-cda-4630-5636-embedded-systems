Download Link: https://assignmentchef.com/product/solved-project-2-cda-4630-5636-embedded-systems
<br>
Assume that the dictionary can have eight entries (index 3 bits) and the eight entries are selected based on frequency (the most frequent instruction should have index 000). If two entries have same frequency, priority is given to the one that appears first in the original program order. The original code consists of 32-bit binaries. You are allowed to use only seven possible formats for compression (as outlined below). Note that if one entry (32-bit binary) can be compressed in more than one way, choose the most beneficial one i.e., the one that provides the shortest compressed pattern. If two formats produce exactly the same compression, choose the one that appears earlier in the following listing (e.g., <em>run-length encoding</em> appears earlier than <em>direct matching</em>). Please count the starting location of a mismatch from the leftmost (MSB) bit of the pattern – the position of the leftmost bit is 00000.




Format of the Run Length Encoding (RLE)

<table width="656">

 <tbody>

  <tr>

   <td width="43">000</td>

   <td width="613">Run Length Encoding (2 bits)</td>

  </tr>

 </tbody>

</table>




Format of bitmask-based compression – starting location is counted from left/MSB

<table width="656">

 <tbody>

  <tr>

   <td width="43">001</td>

   <td width="209">Starting Location (5 bits)</td>

   <td width="228">Bitmask (4 bits)</td>

   <td width="176">Dictionary Index (3 bits)</td>

  </tr>

 </tbody>

</table>




Format of the 1 bit Mismatch – mismatch location is counted from left/MSB

<table width="656">

 <tbody>

  <tr>

   <td width="43">010</td>

   <td width="210">Mismatch Location (5 bits)</td>

   <td width="403">Dictionary Index (3 bits)</td>

  </tr>

 </tbody>

</table>




Format of the 2 bit consecutive mismatches – starting location is counted from left/MSB

<table width="656">

 <tbody>

  <tr>

   <td width="43">011</td>

   <td width="210">Starting Location (5 bits)</td>

   <td width="403">Dictionary Index (3 bits)</td>

  </tr>

 </tbody>

</table>




Format of the 2 bit mismatches anywhere – Mismatch locations (ML) are counted from left/MSB

<table width="656">

 <tbody>

  <tr>

   <td width="43">100</td>

   <td width="210">1<sup>st</sup> ML from left (5 bits)</td>

   <td width="227">2<sup>nd</sup> ML from left (5 bits)</td>

   <td width="176">Dictionary Index (3 bits)</td>

  </tr>

 </tbody>

</table>




Format of the <em>Direct Matching</em>

<table width="254">

 <tbody>

  <tr>

   <td width="43">101</td>

   <td width="211">Dictionary Index (3 bits)</td>

  </tr>

 </tbody>

</table>




Format of the <em>Original Binaries</em>

<table width="656">

 <tbody>

  <tr>

   <td width="43">111</td>

   <td width="613">Original Binary (32 bits)</td>

  </tr>

 </tbody>

</table>




<strong> </strong>

<strong>Run-Length Encoding (RLE) </strong>can be used when there is consecutive repetition of the same instruction. The first instruction of the repeated sequence will be compressed (or kept uncompressed if it is not part of the dictionary) as usual. The remaining ones will be compressed using RLE format shown above. The two bits in the RLE indicates the number of occurrences (00, 01, 10 and 11 imply 1, 2, 3 and 4 occurrences, respectively), excluding the first one. A single application of RLE can encode up to 4 instructions. Assume that the longest sequence can be at most 5 repeating instructions (the first one using other formats and the last 4 using RLE). Note that, RLE should be used when it is profitable compared to other available options.




You are expected to implement the compression and decompression functions using C, C++ or Java. You need to show a working prototype that will take any 32-bit binary (0/1 text) file and compress it to produce a output file that shows compressed patterns arranged in a sequential manner (32-bit in each line, last line padded with 1’s, if needed), a separation marker “xxxx”, followed by eight dictionary entries. Your program should also be able to accept a compressed file (in the above format) and decompress to generate the decompressed (original) patterns. Please see the sample files posted in the webpage.




<strong><u>Command Line and Input/Output Formats</u>: </strong>The simulator should be executed with the following command line. Please use parameters “1” and “2” to indicate compression, and decompression, respectively.<strong>  </strong>

<strong>./SIM</strong>  <strong>1</strong>  (or  <strong>java SIM  1</strong>)<strong>  </strong>for compression

<strong>./SIM</strong>  2  (or  <strong>java SIM  2</strong>) <strong> </strong>for decompression

Please hardcode the input and output files as follows:

<ol>

 <li>Input file for your compression function: <strong>txt   </strong></li>

 <li>Output produced by your compression function: <strong>txt</strong></li>

 <li>Input file for your decompression function: <strong>txt</strong></li>

 <li>Output produced by your decompression function: <strong>txt</strong></li>

</ol>

<strong><u>Submission Policy:</u> </strong>

Please follow the submission policy outlined below. There will be up to 10% <strong>score penalty</strong> based on the nature of submission policy violations.

<ol>

 <li>Please submit only one source file. <strong>Please add “.txt” at the end of your filename</strong>. Your file name must be SIM (e.g., SIM.c.txt <strong>or</strong>cpp.txt <strong>or</strong> SIM.java.txt). On top of the source file, please include the sentence: “/* On my honor, I have neither given nor received unauthorized aid on this assignment */”.</li>

 <li>Please test your submission. These are the exact steps we will follow too.

  <ul>

   <li>Download your submission from eLearning (ensures your upload was successful).</li>

   <li>Remove “.txt” extension (e.g., SIM.c.txt should be renamed to SIM.c)</li>

   <li>Login to <strong>cise.ufl.edu</strong>. If you don’t have a CISE account, go to http://cise.ufl.edu/help/account.shtml and apply for one CISE class account. Then you use <strong>putty</strong> and <strong>winscp</strong> or other tools to login and transfer files.</li>

   <li>Please compile to produce an executable named <strong>SIM</strong>.

    <ul>

     <li>gcc SIM.c –o SIM<strong> or</strong>           javac SIM.java         <strong>or</strong>         g++ SIM.cpp –o SIM            o Please do not print anything on screen.</li>

    </ul></li>

   <li>Assume hardcoded input/output files as outlined in the project description.</li>

   <li>Compress the input file (original.txt) and check with the expected output (compressed.txt)

    <ul>

     <li>./SIM 1 (or java SIM  1)</li>

     <li>diff –w –B cout.txt compressed.txt o Decompress the input file (compressed.txt) and check with the expected output (original.txt)</li>

     <li>./SIM 2 (or java SIM  2)</li>

     <li>diff –w –B dout.txt txt</li>

    </ul></li>

  </ul></li>

</ol>

<ol start="3">

 <li><em>In previous years, there were many cases where output format was different, filename was different, command line arguments were different, or e-Learning submission was missing. All of these led to unnecessary frustration and waste of time for TA, instructor and students. </em><strong>Please use the exactly same commands as outlined above to avoid 10% score penalty. </strong></li>

 <li><strong>You are not allowed to take or give any help in completing this project</strong>. <em>In previous years, some students violated academic honesty (giving help or taking help in completing this project). We were able to establish cheating in several cases – those students received “0” in the project and their names were reported to UF Ethics office. This time we will have <strong>double penalty</strong> for cheating.</em></li>

</ol>




<strong><u>Grading Policy</u></strong>

The class assignments webpage has the sample input and output files. Correct handling of the sample input will be used to determine 60% of credit awarded. The remaining 40% will be determined from other input test cases that you will not have access prior to grading. The other test cases can have different types and number of 32-bit binaries (0/1 text). It is recommended that you construct your own sample input files with which to further test your compression and decompression functions. You can assume that we will use less than 128 32-bit binary (0/1 text) patterns in the new test file. <strong>Please note that the new test case will NOT test any exceptional scenarios that are not described in this document</strong>.