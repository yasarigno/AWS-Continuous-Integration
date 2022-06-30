# AWS-Continuous-Integration
I built an AWS Cloud9 development environment and integrate it with GitHub Actions. The project contains a simple algorithm written in Python. I plan to change it with a more useful one.
Here you will find out what [Continuous Integration](https://aws.amazon.com/devops/continuous-integration/) is.

<p align="center">
<img align="center" src="files\continuous_integration.png" style="width: 400px" />
</p>

## Construction steps to follow :

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
	
# We can do all these together :

all: install lint test
  
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

9. I wrote a simple function. Later on we can change it with a useful code.

```python
def add(x, y):
    return x + y
    
def multiply(x, y):
    return x * y

result = add(1, 2)

print(f"The sum of {1} and {2} is {result}.")

result2 = multiply(3,4)

print(f"The multiple of {3} and {4} is {result2}.")
```
In order to see the results type

```
python hello.py
```

and a test file: 

```python

from hello import add, multiply

def test_add():
    assert add(3, 4) == 7
    
def test_multiply():
    assert multiply(3, 9) == 27
```

10. After writing some code, we can use other commands. ``make format`` will beautify our code; ``make lint`` will check it up; and ``make test`` will run the tests. It is possible to perform all these operations at once using ``make all``.

11. It is time to transfer it to GitHub.

Check out the current status:

```
git status
```

Add all (stage all)

```
git add *
```

Verify that they are now in green by writing ``git status``. **That means they are ready to push**

We now commit it to the main branch

```
git commit -m "adding initial structures"
```

The first time we set up your project, we'll need to do the configuration below either in a file or manually, like I'm going to do it here:

```

git config --global user.name "Your Name"

git config --global user.email you@example.com
  
```

Then this:
```
git commit --amend --reset-author

```
Here we do ``control + O``and ``control + X``

Okay. Hopefully we do not need to do this at every push operation.

It remains to push our files:

```
git push
```

If there are any errors try first ``git pull`` then ``git push``

**Et voilà, finito.**

---

(BONUS)

12. You made change on GitHub, do: ``git pull``

13. You made change on Cloud9, do:

```
git status

git add *

git commit -m "your comment here"

git push
```
That's all.










