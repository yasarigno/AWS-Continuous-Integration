# AWS-Continuous-Integration
I built an AWS Cloud9 development environment and integrate it with GitHub Actions. The project contains a simple algorithm written in Python. I plan to change it with a more useful one.

## Steps to follow :

1. Create the files on Cloud9
2. Delegate GitHub to clone the files from AWS. To do this we need to create an SSH key on Cloud9.

Put this in terminal to generate the key:

```
ssh-keygen -t rsa
```
To get the key:
```
cat /home/ec2-user/.ssh/id_rsa.pub
```
Now copy it to GitHub SSH keys.

3. Clone the files to GitHub.

```
git clone git@github.com:yasarigno/AWS-Continuous-Integration.git
```
Remember that **AWS-Continuous-Integration** was the name of the key inside GitHub.

Now we have a "folder" called AWS-Continuous-Integration on Cloud9. Excellent.

3. Open the folder AWS-Continuous-Integration

```
cd AWS-Continuous-Integration/
```
We can see what is inside 
```
ls
```

4. Create the files on Cloud9. We create 4 files.

```
touch Makefile
touch hello.py
touch test_hello.py
touch requirements.txt
```

5. Create a Virtual Environment :

```
python3 -m venv ~/.AWS-Continuous-Integration
```

then activate it (_-m stands for module). I name this new VE as same as I did for the folder i.e. **AWS-Continuous-Integration**

```
source ~/.AWS-Continuous-Integration/bin/activate
```

6. Write the Makefile

First of all, **convert it to tabs**, then write the following steps 

```
install:
	pip install --upgrade pip &&\
		pip install -r requirements.txt
		
format:
	black *.py
	
lint:
	pylint --disable=R,C hello.py
	
test:
	python -m pytest -vv --cov=hello test_hello.py
  
```
7. Write the requirements file

```
pylint
pytest
click
black
pytest-cov
```

8. Install the packages 

```
make install
```
9.





