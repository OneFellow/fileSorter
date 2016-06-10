# fileSorter
# Sorts files at a given directory

import os, time

def date_of_file(filepath):
	file_attr = os.stat(filepath)
	sorted = time.ctime(file_attr.st_atime).split()
	return (sorted[1], sorted[4])

	
def make_folder(dir_path, folder_date):
	folder_path = dir_path + '/' + folder_date[1] + '_' + folder_date[0].lower()
	try:
		os.mkdir(folder_path)
		return folder_path
	except WindowsError:
		return folder_path

def sort_files():
	directory = raw_input('Which folder would you like to sort? ')
	directory_list = os.listdir(directory)
	for i in directory_list:
		file_name = directory + '/' + i
		folder_name = make_folder(directory, date_of_file(file_name))
		os.renames(file_name, folder_name + '/' + i)
	print len(directory_list), 'files sorted'

sort_files()
