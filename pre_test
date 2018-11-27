# all imports here
import os
import re
import itertools
import threading
import time
import sys
import platform
try:
    import httplib
except:
    import http.client as httplib

path = os.getcwd()

# function check the internet connection
def have_internet():
    conn = httplib.HTTPConnection("www.google.com", timeout=1)
    try:
        conn.request("HEAD", "/")
        conn.close()
        return 'ON'
    except:
        conn.close()
        return 'OFF'

#function for time lag to check internet connection
done = False
def animate():
    for c in itertools.cycle(['|', '/', '-', '\\']):
        if done:
            break
        sys.stdout.write('\rCheck internet connection ' + c)
        sys.stdout.flush()
        time.sleep(0.1)
    sys.stdout.write('\rDone!     ')


# MAIN=> function used to extract protein sequence from the file
def extractlines(file):
	path = os.getcwd()
	new_file = 'sub__'+file+'.csv'
	# open the file downloaded and unzipped
	with open(os.path.join(path,file), encoding = "utf-8") as file:
		# open another new_file is write mode to append data to it
		# new_file = sub__SRR7145317.fastq.csv
		with open(os.path.join(path,new_file), 'a',encoding = "utf-8") as new_file:
			for e, i in enumerate(file):
				# caputring lines only with protein seq
				# here odd line but in file even lines selected (as start is from '0')
				if e%2 != 0:
					# regular expression to find all the charectors from A-Z only
					# join all found and omitting the other remaining char
					i = "".join(re.findall("[A-Z]+", i))
					# append to the new_file created
					print(new_file.write(i),new_file.write("\n"))


print("Automatic download, unzippping and data extraction is active for linux system ONLY.")
print("For windows system download the file and then run the code.")
print("Operating System active: ",platform.platform())
op = input("Enter W for 'Windows' & L for 'Linux' to choose: ")

# condition to check if OS is Linux
if op == 'L' or op == 'l':
	print("Make sure your system is connected to Internet.")
	# small animation to make sure the net connection is active
	t = threading.Thread(target=animate)
	t.start()
	time.sleep(2)
	done = True
	# stat takes the status of internet 
	stat = have_internet()
	# if internet active
	if stat == 'ON':
		print("\nInternet Status: ", stat)
		print("Please wait while the file is being downloaded.")
		# download the file
		os.system("wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR714/007/SRR7145317/SRR7145317.fastq.gz")
		print("Your file has successfully downloaded at loc: ", path)
		print("Please wait while downloaded file is being unzipped.")
		# unzip the file
		os.system("gunzip SRR7145317.fastq.gz")
		# directly taking the file of concern
		# Here it can be made as per user input also
		file = 'SRR7145317.fastq'
		file_path = os.path.join(path, file)
		# checking if file exsists in the required location
		f = os.path.isfile(file_path)
		# if file exsists
		if f == True:
			print("Please wait while your data is being collected in sub__SRR7145317.fastq.csv")
			file = 'SRR7145317.fastq'
			# extract the data
			extractlines(file)
			# open the file in terminal to view
			os.system('less sub__SRR7145317.fastq.csv')
		# if file not found
		else:
			print('File not found. Check Directory alignment.')
	# if internet connection not avaiable
	else:
		print("Internet Status: ", stat)
		print("Connect Internet and retry.")

# condition to check if OS is Windows
elif op == 'W' or op == 'w':
	file = 'SRR7145317.fastq'
	file_path = os.path.join(path, file)
	# checking if file exsists in the required location
	f = os.path.isfile(file_path)
	# if file exsists
	if f == True:
		print("Please wait while your data is being collected in sub__SRR7145317.fastq.csv")
		file = 'SRR7145317.fastq'
		# extract the data
		extractlines(file)
		# open the file in terminal to view
		os.system('less sub__SRR7145317.fastq.csv')
	# if file not found
	else:
		print("File not found")
		print("Please download and unzipped SRR7145317.fastq")
		print("Keep the file in the same directory as the python program")
		print("Then re-run the code")
