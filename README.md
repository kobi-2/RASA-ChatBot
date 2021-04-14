# RASA Chat Bot

Chat Bot using RASA | [Web Link](https://rasa.com/docs/) |  [Github Link](https://github.com/RasaHQ/rasa) 

Rasa is a chatbot framework for voice or text conversation. It is open source. This framework learns using machine learning and can be an automated assistant for many task and on many platforms!

## Contents:
- [Setting up the environment](#setting-up-the-environment)
  * [[Optional] Setting Up a Virtual Environment](#optional-setting-up-a-virtual-environment)
- [Installing RASA](#installing-rasa)
- [Initializing RASA](#initializing-rasa)
- [Training](#training)
  * [Customizing Training Data](#customizing-training-data)
- [Chat](#chat)
- [Example: Trained on Custom Data](#example-trained-on-custom-data)



## Setting up the environment

Getting the latest updates of the global environment:

```
!sudo apt update
!sudo apt install python3-dev python3-pip
```



### [Optional] Setting Up a Virtual Environment

This is an optional step, but recommended because it is safer and cleaner to install packages for special projects in virtual environment rathe than in global system.

```
!apt-get install python3.7-dev python3.7-venv
!python3 -m venv ./venv
```

and run the venv virtual environment:

```
!source ./venv/bin/activate
```



## Installing RASA

Firstly and optionally, we will install the latest pip

```
!pip3 install -U pip
```

Now, we will install rasa using pip

```
!pip3 install rasa
!rasa --version
```



## Initializing RASA

Making directory to have all the necessary rasa files together. 

Moving (changing directory) into rasa directory so that when we try to initialize it and the prompt asks if we want to save the necessary files in that directory, we can say yes.

```
!mkdir rasa
%cd rasa/
```



Initializing RASA is important, because it creates the necessary directories and files.

To initialize RASA:

```
!python -m rasa init
```



This command is a simple do-all command: it basically sets up the assistant. It creates new project, actions, necessary files in the specified directory, and can train given the permission, followed by a chat thread to begin conversation.

When running this command, it will give 3 prompts:

Prompt 1: if we want to save the init files in this present working directory

Prompt 2: if we want to train the model now

Prompt 3: if we would like to start the chat now



We can manually put input to each prompt as they come along when running the above command.

However, to simplify, we can provide the answers right away in the command line with that command by pipelining:

```
!printf '\nN\n' | python -m rasa init
```

​	this means, \n = enter = yes to the 1st prompt, and N\n = No to the 2nd prompt.

or,

```
!printf '\n\nN\n' | python -m rasa init
```

​	this means, \n = enter = yes to the 1st & 2nd prompt, and N\n = No to the 3rd prompt.





Note: If you do not pass the Y/N prompt in the command line with rasa init command, be sure to do so manually when prompted. 

In google colab, the prompt does not show, but instead there is a warning saying your terminal doesn't support cursor position requests (CPR). That means this prompt is waiting for an input.



## Training

To train a model:

```
!rasa train
```



### Customizing Training Data

There are 3 important files, that need to be modified if we want create a custom RASA Chat Bot or an Assistant:

1. **nlu.yml** (in the /data/ directory) : this records the intents (conversation subjects) and their examples.

2. **domain.yml** : this contains possible replies to the intents.

3. **stories.yml** (in /data/ directory) : this contains outlines for stories, which are some example conversation flow. this brings intents from nlu.yml and replies from domain.yml together.

There is another file (in /data/ directory) called **rules.yml**, which specifies rules to follow the conversation path no matter what the previous conversation was, such as, the assistant will say goodbye every time the user says goodbye. 

We have created a custom scenario in this chatbot and data for that. The details are in [this section](#customizing-training-data)

## Chat

To start a chat thread with the rasa assistant with trained data:

```
!rasa shell
```



## Example: Trained on Custom Data 

Custom scenario:

In this GitHub repo, [RASA-ChatBot](https://github.com/kobi-2/RASA-ChatBot), we created a custom RASA Chat Bot Data. It acts as a helpdesk for applying to an internship.


```
An example of the conversation:

- Hi 

RASA: Hey, how may I help you?

- Do you have any internship? 

RASA: yes

- what company is it? 

RASA: ABC company limited.

- What is the job?

RASA: you will be learning and helping to implement various ML tasks in practical real life scenarios.

- How can I apply? 

RASA: you can send your cv at hr@abc.com. Upon that, you will be asked to complete an online form with some simple technical tasks, followed by an interview and another task. That is all! 

```

For this, we changed in 4 files: 

1. nlu.yml [[github link](https://github.com/kobi-2/RASA-ChatBot/blob/main/rasa/data/nlu.yml)]

2. domain.yml [[github link](https://github.com/kobi-2/RASA-ChatBot/blob/main/rasa/domain.yml)]

3. stories.yml [[github link](https://github.com/kobi-2/RASA-ChatBot/blob/main/rasa/data/stories.yml)]

4. rules.yml [[github link](https://github.com/kobi-2/RASA-ChatBot/blob/main/rasa/data/rules.yml)]



