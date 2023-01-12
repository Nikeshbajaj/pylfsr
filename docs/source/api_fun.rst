API: Supporting Functions
========================

Supporting Functions for Linear Feedback Shift Register

Primitive Polynomials
--------------------

.. raw:: html
   
   <p style="border-width:1px; border-style:solid; border-color:#99e6FF; padding: 1em;">
      get_fpolyList(m=None)<br>
      
      Get the list of primitive polynomials as feedback polynomials for m-bit LFSR.
      Only half list of primary primitive polynomials are retuned, not the full list (half list), since for each primary primitive polynomial
      an image polymial can be computed using 'get_Ifpoly' method
   </p>


**get_fpolyList(m=None)**
 
Get the list of primitive polynomials as feedback polynomials for m-bit LFSR.
Only half list of primary primitive polynomials are retuned, not the full list (half list), since for each primary primitive polynomial
an image polymial can be computed using 'get_Ifpoly' method

Parameters: 
   m: 1<int<32, if None, list of feedback polynomials for 1 < m < 32 is return as a dictionary

Returns: 
   fpoly_list: list of polynomial if m is not None else a dictionary

Example:
   
   .. code:: python

      import pylfsr as PYL
      #returns a dictionary of polynomial
      polylist = PYL.get_fpolyList(m=None)

      #returns list of polynomial for m-bit LFSR
      polylist = PYL.get_fpolyList(m=5)

      print(polylist)
      [[5, 2], [5, 4, 2, 1], [5, 4, 3, 2]]


Image Replica of a polynomial
--------------------

.. raw:: html
   
   <p style="border-width:1px; border-style:solid; border-color:#99e6FF; padding: 1em;">
      get_Ifpoly(fpoly)
      
      Get image replica of feebback polynomial
   </p>



**get_Ifpoly(fpoly)**


Parameters: 
     fpoly: polynomial as list e.g. [5,2] for x^5 + x^2 + 1
          : should be a valid primitive polynomial

Returns:
     ifpoly: polynomial as list e.g. [5,3] for x^5 + x^3 + 1

Example

.. code:: python

   import pylfsr as PYL

   #returns image polynomial of given polynomial
   ipoly = PYL.get_Ifpoly([5, 4, 2, 1])

   print(ipoly)
   [5, 4, 3, 1]



Display LFSR
--------------------

.. raw:: html
   
   <p style="border-width:1px; border-style:solid; border-color:#99e6FF; padding: 1em;">
      dispLFSR(state, fpoly, conf='fibonacci', seq='', out_bit_index=-1, ob=None, fb=None, fs=25, ax=None, 
           show_labels=False, title='', title_loc='left', box_color='lightblue', alpha=0.5, 
           output_arrow_color='C0', output_arrow_style='h')
   </p>



.. function:: 

 dispLFSR(state, fpoly, conf='fibonacci', seq='', out_bit_index=-1, ob=None, fb=None, fs=25, ax=None, 
           show_labels=False, title='', title_loc='left', box_color='lightblue', alpha=0.5, 
           output_arrow_color='C0', output_arrow_style='h')
    

Display LFSR for given state, fpoly and conf.
    
Parameters:
   
   state: current state of LFSR
   fpoly:  feedback polynomial of LFSR
   seq: str, output sequence
   ob: output bit
   fb: feedback bit
   ax: axis to plot, if None, new axis will be created, (default None)
   show: if True, plt.show() will be excecuted, (default True)
   fs:  fontsize (default 25)
   show_label: if true, will display names
   title: str, title of figure, default '',
   title_loc, alignment of title, 'left', 'right', 'center', (default 'left')
   box_color: color of register box, default='lightblue'

    
Example:
   
.. code:: python
      
      import pylfsr as PYL
      
      PYL.dispLFSR(state=[1,1,1,1,0], fpoly=[5,3], conf='fibonacci', seq='111', title='R1')


Lempel-Ziv Complexity
--------------------

.. raw:: html
   
   <p style="border-width:1px; border-style:solid; border-color:#99e6FF; padding: 1em;">
      lempel_ziv_complexity(seq)<br>
   </p>

**lempel_ziv_complexity(seq):**
    
   Lempel-Ziv Complexity.

   It is defined as the number of different patterns exists in a given stream.

   As an example:
   s = '1001111011000010'
   patterns ==> 1, 0, 01, 11, 10, 110, 00, 010
   #patterns = 8

   Parameters:

      seq: as string of sequence, could be binary or any other

   Returns:

      lc: number of different patterns in LZ dictionary


Example:
   
   .. code:: python

      import pylfsr as PYL
      from pylfsr import LFSR
      
      L = LFSR()
      L.runKCycle(100)
      seq = L.getSeq()
      lc = PYL.lempel_ziv_complexity(seq)
      print(lc)
      
      29
      

--     


.. raw:: html
   
   <p style="border-width:1px; border-style:solid; border-color:#99e6FF; padding: 1em;">
      lempel_ziv_patterns(seq)<br>
   </p>

**lempel_ziv_patterns(seq)**:
    
   Lempel-Ziv patterns. 
   
   It is defined as a set of different patterns exists in a given sequence.

   As an example:
   s = '1001111011000010'
   patterns ==> 1, 0, 01, 11, 10, 110, 00, 010

   Parameters:      
      seq: as string of sequence, could be binary or any other

   Returns:

      dictionary of all the LZ patterns in given sequence




Example:
   
   .. code:: python

      import pylfsr as PYL
      from pylfsr import LFSR
      
      L = LFSR()
      L.runKCycle(100)
      seq = L.getSeq()
      pdict = PYL.lempel_ziv_patterns(seq)
      print(pdict)
      
      {'0',
       '00',
       '000',
       '0001',
       '00010',
       '001',
       '0011',
       '01',
       '010',
       '0100',
       '0101',
       '011',
       '0111',
       '1',
       '10',
       '100',
       '1000',
       '101',
       '1011',
       '10110',
       '101100',
       '11',
       '110',
       '1100',
       '1101',
       '11010',
       '11011',
       '111',
       '1111'}

