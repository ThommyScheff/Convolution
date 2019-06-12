#!/usr/bin/env python
"""
Convolution is a mathematical operation on two functions which produces a third function that expresses how the shape of one is modified by the other. It contains the discrete convolution with only valid outputs or the whole output with out of bound values.
"""
__author__ = "Thommy Scheffner"
__copyright__ = "Copyright 2019, Goethe University for DocStrings"
__credits__ = ["Thommy Scheffner"]

__license__ = "GPL"
__version__ = "3.7.3"
__maintainer__ = "Thommy Scheffner"
__email__ = "itzthommy@gmx.de"
__status__ = "Completed"

class signal():
    def __init__(self, values):
        """Constructor for signal
        DO NOT MODIFIY THIS METHOD"""
        self.values = values

    def __str__(self):
        """Returns the signal as a string representation,
        every value should be rounded to 2 decimal places
        and separated from other values by a space. See example
        testcase for further guidance."""
        toReturn = ''
        if self.values == [[]]:
            return None
                
        else:
            for i in range(len(self.values)):
                toReturn += "%.2f" % self.values[i]
                if i != len(self.values) - 1 :
                    toReturn += ' '
        return toReturn


    def convolve(self, inputSignal):
        """Convolves the signal with another signal. Only
        valid convolutions are performed, i.e. the length of the
        output signal is the length of self.
        
        Any value outside of either signal is assumed to be 0.
        

        You may assume that all signals have an
        odd length. See example testcase for further guidance.
        """

        max_length = int
        n_length = len(self.values)
        m_length = len(inputSignal.values)
        max_length = (n_length + m_length) -1

        first = signal([])
        oob_list = signal([])
        outputSignal = signal([])
        for i in range(len(self.values)): 
            x = self.values[i]   
            first.values.append(x)

        for i in range(len(inputSignal.values)): 
            x = inputSignal.values[i]   
            oob_list.values.append(x)

        for n in range(max_length):
            x = 0
            
            for m in range(len(self.values)):
                try:
                    if (n-m < 0):
                        x += 0
                    
                    else:
                        x += first.values[m] * oob_list.values[n-m]

                except IndexError:
                    x += 0                    
                                   
            outputSignal.values.append(x)
            
            
        while len(self.values) != len(outputSignal.values):
                del outputSignal.values[0]
                del outputSignal.values[-1]     
    
        return outputSignal
            

    def convolveFull(self, inputSignal):
        """Convolves the signal with another signal. All
        relevant (as soon as signals overlap) convolutions are performed,
        i.e. the length of the output signal depends on the length
        of self and the input signal.

        Any value outside of either signal is assumed to be 0.
        

        You may assume that all signals have an
        odd length. See example testcase for further guidance.
        """
        
        max_length = int
        n_length = len(self.values)
        m_length = len(inputSignal.values)
        max_length = (n_length + m_length) -1

        first = signal([])
        oob_list = signal([])
        outputSignal = signal([])
        for i in range(len(self.values)): 
            x = self.values[i]   
            first.values.append(x)

        for i in range(len(inputSignal.values)): 
            x = inputSignal.values[i]   
            oob_list.values.append(x)

        for n in range(max_length):
            x = 0
            
            for m in range(len(self.values)):
                try:
                    if (n-m < 0):
                        x += 0
                    
                    else:
                        x += first.values[m] * oob_list.values[n-m]
                except IndexError:
                    x += 0

            outputSignal.values.append(x)
 
        return outputSignal
