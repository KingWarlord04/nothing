#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>
#include <iomanip>
using namespace std;

int MAX_RECORDS = 300;
const int CATEGORIES = 5;
bool program_runs = true;

int size_calculator(string file_path){
	ifstream read_file(file_path.c_str());
	string file_test;
	int number_records=0;
	
	if(read_file.fail())
	{
		cout << " File does not exist!\n"; 
	}
	else
	{
		getline(read_file, file_test);
		getline(read_file, file_test);
		while(getline(read_file, file_test))
		{
			number_records++;
		}	
	}
	read_file.close();
	
	return number_records;
}

void array_maker(string *array1, string *array2, string *array3, double *array4, double *array5, int rec_size, string column_name[], string file_path)
{
	ifstream read_file(file_path.c_str());
	string file_test;
	int i = 0;
	
	if(read_file.fail())
	{
		cout << "File does not exist!\n";
	}
	else
	{
		getline(read_file, file_test);
		getline(read_file, file_test);
		while(read_file >> array1[i] >> array2[i] >> array3[i] >> array4[i] >> array5[i])
		{
			i++;
		}
	}
	read_file.close();
	
	cout << fixed << setprecision (1);
	cout << "\t+-----------------------------------------------------------------------------------+\n";
	
	for(int i=0; i < CATEGORIES; i++){
		cout << setw(9) << "|" << column_name[i];
	}
	cout << "  |\n\t";
	cout << "+-----------------------------------------------------------------------------------+\n";
	
	//for(int i = 0; i < rec_size; i++)
	//{
		//cout << "\t";
	for(int j = 0; j < rec_size; j++)
	{
		cout << "\t|" << array1[j] << "    |" << array2[j] << "\t      |" << array3[j] << "\t\t |" << array4[j] << "\t\t     |" << array5[j] << "\t    |"<< endl;
		cout <<  "\t-------------------------------------------------------------------------------------\n";
	}
	//}
	cout << endl;
}

void name_search(string l_name, string *lname_array, int rec_size, string *array1, string *array3, double *array4, double *array5)
{
	int size, matches = 0;
	for(size = 0; size < rec_size ; size++)
	{
		if(l_name == lname_array[size])
		{
			matches++;
			cout << "\n\tResult No." << matches << endl;
			cout << "\n\tID: " << array1[size] << "\n\tLast Name: " << lname_array[size] << "\n\tFirst Name: " << array3[size] << "\n\tHourly Rate: $" << array4[size] << "\n\tHours Worked this Month: " << array5[size] << endl;
		}
	}
	if(matches == 0)
	{
		cout << "\nRecord not found in the database!\n";
	}
}
int main(){

	string path = "/Users/lbasi/Downloads/StaffDetails.txt";
	
	int size = size_calculator(path);
	
	string test;
	
	string column_names[CATEGORIES] = {"IDS", "Last Name", "First Name", "Hourly Rate", "Hours Worked"};
	string ids[MAX_RECORDS], last_name[MAX_RECORDS], first_name[MAX_RECORDS];
	double hourly_rates[MAX_RECORDS], hours_worked[MAX_RECORDS];
	

	
		array_maker(ids, last_name, first_name, hourly_rates, hours_worked, size, column_names, path);
		name_search("Bond", last_name, size, ids, first_name, hourly_rates, hours_worked);
	
	
	
	
	return 0;
	
}
