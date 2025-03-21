# tinytroupe-test2

## Step 1: Install Packages

Open a terminal from Codespace on Github. In the terminal, run the following command to clone the repository:

```bash
git clone https://github.com/microsoft/tinytroupe
```

Change directory into the `tinytroupe` folder:

```bash
cd tinytroupe
```

Install the package:

```bash
pip install .
```

## Step 2: Setup API Key

In the terminal that you just installed packages, use the following command to setup API Key:

```bash
export OPENAI_API_KEY="xxxx"
```

## Step 3: Experiments (Simulation)

### Talk to an existing persona

```python
from tinytroupe.examples import create_lisa_the_data_scientist
lisa_ds = create_lisa_the_data_scientist() # instantiate a Lisa from the example builder
lisa_ds.listen_and_act("Tell me about your life.")
```

### Talk to a customized persona

This implies you need to define a new persona using `tinytroupe` package.

```python
from tinytroupe.agent import TinyPerson

yiqiao = TinyPerson("Yiqiao")
yiqiao.define("age", 35)  # Adjust the age as per your requirement
yiqiao.define("nationality", "Chinese")
yiqiao.define("occupation", "He is a professor in a university.")
```

Use the method `.listen_and_act` to have a conversation with the persona you defined above

```python
yiqiao.listen_and_act("Tell me about yourself.")
```

### Observe a conversation between two personas

This implies you have at least two personas defined. Since we already defined one above, let us define another one.

```python
from tinytroupe.agent import TinyPerson

john = TinyPerson("John")
john.define("age", 22)  # Adjust the age as per your requirement
john.define("nationality", "American")
john.define("occupation", "He is a student in a university.")
```

To instantiate a conversation between two personas above, you will need `TinyWorld` function.

```python
from tinytroupe.environment import TinyWorld

world = TinyWorld("Classroom", [yiqiao, john])
world.make_everyone_accessible()

yiqiao.listen("I want to extend my homework.")
world.run(3) # trigger the conversation with 3 rounds back-and-forth
```

## Questions need to be answered:

1. How to install `tinytroupe` packages?
2. What is Turing Test? In today's world with Large Language Models (LLMs), what is the definition of Turing Test?
3. Create a simulation of your own topic and show me the transcript. This implies define at least two personas of your own choice with conflict built in and observe their conversation. You can simply copy/paste the conversation in a `.md` file. Please comment on the transcript whether you think the Turing Test is passed.

---
For question 3, I would expect your submission to look like the following.

The following is my conversation:

```bash
>>> world = TinyWorld("Classroom", [yiqiao, john])
>>> world.make_everyone_accessible()
>>> yiqiao.listen("I want an extension to my homework.")
USER --> Yiqiao: [CONVERSATION] 
          > I want an extension to my homework.
TinyPerson(name='Yiqiao')
>>> world.run(3)
───────────────────────────────────────────────────────────────────────────────────── Classroom step 1 of 3 ──────────────────────────────────────────────────────────────────────────────────────
Yiqiao acts: [THINK] 
            > A student is asking for an extension on their homework again. I need to remember the
            > previous context and consider their situation before responding.
Yiqiao acts: [TALK] 
            > Can you remind me why you need an extension on your homework? I want to understand
            > your situation better this time.
Yiqiao acts: [DONE] 

Yiqiao --> John: [CONVERSATION] 
            > Can you tell me why you need an extension on your homework this week? I want to
            > understand your situation better.
Yiqiao --> John: [CONVERSATION] 
            > I understand that you're very busy with work and family responsibilities. Given your
            > situation, I can grant you an extension on your homework this week. Please make sure
            > to submit it as soon as you can.
Yiqiao --> John: [CONVERSATION] 
            > Can you remind me why you need an extension on your homework? I want to understand
            > your situation better this time.
John acts: [THINK] 
          > I need to explain my situation to Yiqiao clearly. Balancing work and family is tough,
          > and I want to make sure he understands why I need this extension.
John acts: [TALK] 
          > I appreciate your understanding, Yiqiao. I'm currently juggling a demanding work
          > schedule and taking care of my two young kids, which has made it challenging to keep up
          > with my homework. I want to ensure I submit quality work, so an extension would really
          > help me out.
John acts: [DONE] 

John --> Yiqiao: [CONVERSATION] 
          > I appreciate your understanding, Yiqiao. I'm currently juggling a demanding work
          > schedule and taking care of my two young kids, which has made it challenging to keep up
          > with my homework. I want to ensure I submit quality work, so an extension would really
          > help me out.
───────────────────────────────────────────────────────────────────────────────────── Classroom step 2 of 3 ──────────────────────────────────────────────────────────────────────────────────────
Yiqiao acts: [THINK] 
            > John is facing a tough situation with his work and family responsibilities. His
            > request for an extension is reasonable given his circumstances. I should consider
            > granting it to support him while maintaining the quality of work expected in my class.
Yiqiao acts: [TALK] 
            > Thank you for sharing your situation, John. I understand how challenging it can be to
            > balance work and family. I will grant you an extension on your homework to help you
            > submit quality work. Please make sure to submit it as soon as you can.
Yiqiao acts: [DONE] 

Yiqiao --> John: [CONVERSATION] 
            > Thank you for sharing your situation, John. I understand how challenging it can be to
            > balance work and family. I will grant you an extension on your homework to help you
            > submit quality work. Please make sure to submit it as soon as you can.
John acts: [THINK] 
          > I'm grateful that Yiqiao understands my situation and has granted me the extension. This
          > will really help me manage my workload better.
John acts: [TALK] 
          > Thank you so much, Yiqiao! I really appreciate your understanding and support. I will
          > make sure to submit my homework as soon as I can.
John acts: [DONE] 

John --> Yiqiao: [CONVERSATION] 
          > Thank you so much, Yiqiao! I really appreciate your understanding and support. I will
          > make sure to submit my homework as soon as I can.
───────────────────────────────────────────────────────────────────────────────────── Classroom step 3 of 3 ──────────────────────────────────────────────────────────────────────────────────────
Yiqiao acts: [THINK] 
            > John is grateful for the extension, which is good to see. I hope he can manage his
            > time well and submit quality work. It's important for students to feel supported while
            > also maintaining academic standards.
Yiqiao acts: [DONE] 

John acts: [DONE] 
```

Here's my comment: I think the bots passed the Turing Test. Here's why xxxxx.