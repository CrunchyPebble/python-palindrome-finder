import sys
from PyQt5 import QtWidgets
from PyQt5.QtCore import pyqtSlot
from PyQt5.QtWidgets import QApplication, QDialog, QTableWidget, QTableWidgetItem
from PyQt5.uic import loadUi
import enchant
from PyQt5.uic.properties import QtGui

vowels = ['a', 'e', 'i', 'o', 'u']

dictionary = enchant.Dict("en_US")

class PalindromeUI(QDialog):
    def __init__(self):
        super(PalindromeUI, self).__init__()
        loadUi('PalindromeUI.ui', self)
        self.setWindowTitle('PalindromeFinder')
        self.btnFind.clicked.connect(self.on_find_clicked)
       #self.btnClear.clicked.connect(self.on_clear_clicked)

    @pyqtSlot()
    def on_find_clicked(self):
        #clearing all rows beforehand
        while (self.tblPalindrome.rowCount() > 0):
            self.tblPalindrome.removeRow(0)

        #getting the word
        strWord = str(self.txtInput.text()).lower()

        #creating blank template arrays for future appendages
        repeatedLetters = []
        consonantsInWord = []
        vowelsInWord = []

        threeLetter = []
        fourLetter = []
        fiveLetter = []


        # adding all the consonants and vowels of the word into different arrays
        for letter in strWord:
            if letter in vowels:
                vowelsInWord.append(letter)
            else:
                consonantsInWord.append(letter)

        # three letter palindromes
        for consonant in consonantsInWord:
            for vowel in vowelsInWord:
                possibleWord = consonant + vowel + consonant
                possibleWord2 = vowel + consonant + vowel
                boolean = dictionary.check(possibleWord)
                boolean2 = dictionary.check(possibleWord2)
                if boolean == True:
                    if possibleWord not in threeLetter:
                        threeLetter.append(possibleWord)
                    else:
                        break
                if boolean2 == True:
                    if possibleWord2 not in threeLetter:
                        threeLetter.append(possibleWord2)
                    else:
                        break

        # four letter palindromes
        for consonant in consonantsInWord:
            for vowel in vowelsInWord:
                possibleWord = consonant + vowel + vowel + consonant
                possibleWord2 = vowel + consonant + consonant + vowel
                boolean = dictionary.check(possibleWord)
                boolean2 = dictionary.check(possibleWord2)
                if boolean == True:
                    if possibleWord not in fourLetter:
                        fourLetter.append(possibleWord)
                    else:
                        break
                if boolean2 == True:
                    if possibleWord2 not in fourLetter:
                        fourLetter.append(possibleWord2)
                    else:
                        break

        # five letter palindromes
        for consonant in consonantsInWord:
            for vowel in vowelsInWord:
                for anotherConsonant in consonantsInWord:
                    for anotherVowel in vowelsInWord:
                        possibleWord = consonant + vowel + anotherConsonant + vowel + consonant
                        possibleWord2 = vowel + consonant + anotherVowel + consonant + vowel
                        boolean = dictionary.check(possibleWord)
                        boolean2 = dictionary.check(possibleWord2)
                        if boolean == True:
                            if possibleWord not in fiveLetter:
                                fiveLetter.append(possibleWord)
                            else:
                                break

                        if boolean2 == True:
                            if possibleWord2 not in fiveLetter:
                                fiveLetter.append(possibleWord2)
                            else:
                                break

        # this is to find out how many rows I need to create
        # the number of rows is the same as the length of the largest set
        if (len(threeLetter) > len(fourLetter)) and (len(threeLetter) > len(fiveLetter)):
            largest = len(threeLetter)
        elif (len(fourLetter) > len(threeLetter)) and (len(fourLetter) > len(fiveLetter)):
            largest = len(fourLetter)
        else:
            largest = len(fiveLetter)

        # inserting all of the palindromes row by row
        for i in range(0, largest):
            numRows = self.tblPalindrome.rowCount()
            self.tblPalindrome.insertRow(numRows)

            if i < len(threeLetter):
                self.tblPalindrome.setItem(numRows, 0, QtWidgets.QTableWidgetItem(threeLetter[i]))

            if i < len(fourLetter):
                self.tblPalindrome.setItem(numRows, 1, QtWidgets.QTableWidgetItem(fourLetter[i]))

            if i < len(fiveLetter):
                self.tblPalindrome.setItem(numRows, 2, QtWidgets.QTableWidgetItem(fiveLetter[i]))

            # clear everything

        @pyqtSlot()
        def on_clear_clicked(self):
            self.txtInput.clear()
            while (self.tblPalindrome.rowCount() > 0):
                self.tblPalindrome.removeRow(0)


app = QApplication(sys.argv)
widget = PalindromeUI()
widget.show()
sys.exit(app.exec_())
