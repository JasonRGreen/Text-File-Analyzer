# Text-File-Analyzer
This program that reads a text file, then prints    some statistical results about its contents to an output file. The    results will be primarily an analysis of the characters in the file
#include <iostream>
#include <fstream>
#include <iomanip>
using namespace std;

	char filename[30];														//input filename
	char filename2[30];														//output filename
	ifstream in1;
	ofstream out1;
	int counter;
	char in;
	int letter=0;															//counter for letters
	int digit=0;															//counter for digits
	int whitespace=0;														//counter for white space
	int other=0;															//counter for nything else
	int total;
	int upper=0;															//counter for uppercase letters
	int lowercase=0;														//counter for lowercase letters
	int alphabet[26]={0};													//an array to represent all letters in the alphabet
	int letter_size = 26;
	const int ANUM = 97;													//ASCII value for 'a'
	const int ZNUM = 122;													//ASCII value for 'z'


int main()
{
	do
	{
		in1.clear();

		cout << "Please enter the name of the input file. \n";				//prompts user to enter text input file
		cout << "Filename : ";
		cin >> filename;

		in1.open(filename);
		if(!in1)															//if user does not enter a text file they must try again
			cout << "Attempt to read file failed. Please try again. \n";

	} while (!in1);

	do
	{
		out1.clear();

		cout << "Please enter the name of the output file. \n";				//prompts user to enter output text file
		cout << "Filename: ";
		cin >> filename2;

		out1.open(filename2);
		if(!out1)															//if user does not enter a text file they must try again
			out1 << "Attempt to read file failed. Please try again. \n";

	} while (!out1);



	do{
		in = in1.get();														//to pull out a character in the file
		 
		if(isalpha(in))														//if the character is a letter
		{
			letter++;														//increment the counter for letter
			if(isupper(in))													//if the letter is uppercase
			{
				upper++;													//increment uppercase counter
				in = tolower(in);											//then change uppercase letters to lowercase letters
			}
			else
				lowercase++;												//if the letter is lowercase increment the lowercase counter
			alphabet[in -ANUM]++;

		}
		else if(isdigit(in))												//if the character is a digit
		{
			digit++;														//increment the digit counter
		}
		else if (isspace(in))												//if the character is blank space increment the black space counter
		{
			whitespace++;
		}
		else
		{                                                                   //if the character is none of those mentioned about increment the other counter
			other++;
		}

	}while(!in1.eof());

	total = letter+digit+whitespace+other;									//to get the total number of characters in the text file

	cout << "Processing is complete.\n";

	/*sets all data to the second decimal point*/
	cout.setf(ios::fixed);
	cout.setf(ios::showpoint);
	cout.precision(2);


	cout << "Statistic for file: " << filename << "\n";
	cout << "----------------------------------------------------------- \n\n";
	cout << "Total # of characters in the file: " << total << "\n";
	cout << "Category \t How many in file \t % of file \n";
	cout << "----------------------------------------------------------- \n";
	cout << "Letters \t"  << setw(15) << letter << " \t" << setw(8) << letter*100/static_cast<float>(total) << " % \n";
	cout << "White Space \t" << setw(15) << whitespace << " \t"<< setw(8) << whitespace*100/static_cast<float>(total)<< " % \n";
	cout << "Digits \t" << setw(23) << digit << " \t" << setw(8) << digit*100/static_cast<float>(total) << " % \n";
	cout << "Other characters \t" << setw(7) << other << " \t" << setw(8) << other*100/static_cast<float>(total) << " % \n";

	cout << "LETTER STATISTICS \n";
	cout << "Category \t  How many in the file \t % of all letters \n";
	cout << "------------------------------------------------------------ \n";
	cout << "Uppercase\t" << setw(15) << upper << "\t" << setw(18) << upper*100/static_cast<float>(letter) << " % \n";
	cout << "Lowercase\t" << setw(15) << lowercase << "\t" << setw(18) << lowercase*100/static_cast<float>(letter) << " % \n";

	/*this loop produces the lteers out of the alphabet*/
	for(int i=0 ; i<letter_size; i++)
		cout << static_cast<char>(ANUM+i) << "\t" << setw(23) << alphabet[i] << "\t" << setw(18) << alphabet[i]*100/static_cast<float>(letter) << " % \n";

	return 0;
}
