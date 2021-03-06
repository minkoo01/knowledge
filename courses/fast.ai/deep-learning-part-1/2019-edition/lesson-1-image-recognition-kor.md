# Lesson 1 - Image Recognition

_These are my personal notes from fast.ai Live (the new International Fellowship programme) course and will continue to be updated and improved if I find anything useful and relevant while I continue to review the course to study much more in-depth. Thanks for reading and happy learning!_ <br>
`이것들은 fast.ai 라이브 (새로운 국제 펠로우쉽 프로그램) 코스의 내 개인적인 노트입니다. 그리고 만약 내가 훨씬 더 심층적으로 공부하기 위해 과정을 계속 검토하는 동안 유용하고 적절한 것을 발견한다면 계속해서 업데이트되고 개선될 것입니다. 독서와 행복한 배움에 감사드립니다!`

Live date: 23 Oct 2018, GMT+8

## Topics

* Introduction and welcome!
* fast.ai course v3 website
* Getting started
  * Using a GPU
  * Jupyter notebook
  * Our forums
  * PyTorch and fastai library
* Server setup
* fastai v1 documentations
* Advice
* Look at the data
* Training
* Transfer learning
* Interpreting the results
* ResNet50
* Homework

## Lesson Resources

* [Course website](https://course.fast.ai/)
* [Lesson 1 video player](https://course.fast.ai/videos/?lesson=1)
* [Video](https://www.youtube.com/watch?v=XfoYk_Z5AkI)
* [Official resources and updates (Wiki)](https://forums.fast.ai/t/lesson-1-official-resources-and-updates/27936)
* [Forum discussion](https://forums.fast.ai/t/lesson-1-chat/27332)
* [FAQ, resources, and official course updates](https://forums.fast.ai/t/faq-resources-and-official-course-updates/27934)
* Jupyter Notebook and code
  * [00_notebook_tutorial.ipynb](https://nbviewer.jupyter.org/github/fastai/course-v3/blob/master/nbs/dl1/00_notebook_tutorial.ipynb)
  * [lesson1-pets.ipynb](https://nbviewer.jupyter.org/github/fastai/course-v3/blob/master/nbs/dl1/lesson1-pets.ipynb)
* [Documentations for the fastai deep learning library](http://docs.fast.ai/)

## Assignments

* Get your GPU going
* Run lesson 1 notebook, `lesson1-pets.ipynb`.
* Build your own image dataset.
  * Try out the different ways of creating datasets.
  * Write a guide on how to do it.
* Replicate lesson 1 notebook:
  * Reuse the code.
  * Repeat process on your own dataset or with a different dataset
* Share your work on forums
  * Get on the forum and tell us any little success you had.
* fastai v1 docs
  * git clone fastai_docs repo
  * run the code
  * experiment

## Other Resources

### Papers

* Optional reading
  * [Oxford-IIIT Pet Dataset by O. M. Parkhi et al., 2012](http://www.robots.ox.ac.uk/~vgg/publications/2012/parkhi12a/parkhi12a.pdf)
  * [Visualizing and Understanding Convolutional Networks by Matt Zeiler et al.](https://cs.nyu.edu/~fergus/papers/zeilerECCV2014.pdf)

### Blog Posts and Articles

* Optional reading
  * [fast.ai software could radically democratize AI](https://www.zdnet.com/article/fast-ais-new-software-could-radically-democratize-ai/)
  * [Cricket vs. Baseball - an example by Nikhil Balaji of what you are going to be able to do by the end of lesson 1](https://forums.fast.ai/t/cricket-or-baseball-lesson-1-with-small-datasets/8097)
  * [AI Can Recognize Images. But Can It Understand This Headline?](https://www.wired.com/story/ai-can-recognize-images-but-understand-headline/)
  * [Towards Natural Language Semantic Code Search by Hamel Husain and team at GitHub Engineering](https://githubengineering.com/towards-natural-language-semantic-code-search/)
  * [fast.ai recent alumni, Christine Payne, now at OpenAI and her project, Clara, a neural network generator](http://christinemcleavey.com/clara-a-neural-net-music-generator/)
  * [One of our other alumni (Sanyam Bhutani) of the course recently interviewed with OpenAI Fellow: Christine McLeavey Payne](https://hackernoon.com/interview-with-openai-fellow-christine-mcleavey-payne-aaef948ad571)
  * [A small team of student AI coders beats Google’s machine-learning code](https://www.technologyreview.com/s/611858/small-team-of-ai-coders-beats-googles-code/)

# My Notes

## Getting Started

Welcome! Practical Deep Learning for Coders lesson 1.

[[0:12](https://youtu.be/BWWm4AzsdLk?t=12)] There's a lesson 0. Lesson 0 is why do you need GPU and how did you get it setup. So if you haven't got a GPU running yet, then go back and do that.

:bulb: _Note: you can also watch this first lesson without following along with a GPU, so you can see how it all works. Then watch a 2nd time after you have a GPU and try to implement the code yourself._

Make sure your GPU environment is set up and you can run Jupyter Notebook. Then you are ready to start the real lesson 1.

[00_notebook_tutorial.ipynb](https://nbviewer.jupyter.org/github/fastai/course-v3/blob/master/nbs/dl1/00_notebook_tutorial.ipynb)

The code is in Python.

Four shortcuts:
- <kbd>Shift</kbd>+<kbd>Enter</kbd>: runs the code or markdown on a cell
- <kbd>Up Arrow</kbd>+<kbd>Down Arrow</kbd>: toggle across cells
- <kbd>b</kbd>: create new cell
- <kbd>0</kbd>+<kbd>0</kbd>: restart kernel

[[2:45](https://youtu.be/BWWm4AzsdLk?t=165)]

Jupyter Notebook is a really interesting device for data scientists because it lets you run interactive experiments and give you not just a static piece of information but something you can interactively experiment with. <br>
`Jupyter Notebook은 데이터 과학자들에게 정말 흥미로운 장치입니다. 왜냐하면 그것은 여러분이 대화형 실험을 할 수 있게 해주고, 단지 정적인 정보들이 아닌 여러분이 대화식으로 실험할 수 있는 어떤 것을 제공하기 때문입니다.`

How to use notebooks and the materials well based on the last three years of experience: <br>
`지난 3년간의 경험을 바탕으로 Notebook과 자료를 잘 사용하는 방법`

1. Just watch a lesson end to end.
   - Don't try to follow along because it's not really designed to go the speed where you can follow along. It's designed to be something where you just take in the information, you get a general sense of all the pieces, how it all fits together. <br>
   `따라갈 수 있는 속도를 따라갈 수 있도록 설계되어 있지 않기 때문에 따라가려고 하지 마십시오. 그것은 여러분이 정보를 얻고, 모든 조각들에 대한 일반적인 감각을 얻으며, 어떻게 모든 것이 서로 맞는지 알기 위해 고안된 것입니다.`
   - Then you can go back and go through it more slowly pausing the video, trying things out, making sure that you can do the things that I'm doing and you can try and extend them to do things in your own way. <br>
   `그리고 나서 여러분은 다시 돌아가서 더 천천히 비디오를 볼 수 있고, 무언가를 시도해 볼 수 있고, 여러분이 내가 하고 있는 일을 할 수 있고, 여러분만의 방식으로 그것들을 확장해 볼 수 있도록 할 수 있습니다.`
   - Don't worry if things are zipping along faster than you can do them. That's normal. <br>
   `일이 당신이 할 수 있는 것보다 더 빨리 진행되고 있는지 걱정하지 마세요. 그런 건 보통이에요.`
   - Don't try and stop and understand everything the first time. If you do understand everything the first time, good for you. But most people don't particularly as the lessons go on, they get faster and they get more difficult. <br>
   `처음부터 모든 것들을 이해하려고 하지 마라. 만약 여러분이 처음부터 모든 것을 이해한다면 좋겠지만, 대부분의 사람들은 특히 수업이 진행될수록 더 빨라지고 더 어려워진다.`

So at this point, we've got our notebooks going. We're ready to start doing deep learning. <br>
`그래서 이 시점에서, 우리는 우리의 notebook을 실행하고 있다. 우리는 deep learning을 시작할 준비가 되어 있다.`

### You can do deep learning [[4:31](https://youtu.be/BWWm4AzsdLk?t=271)]

![](../../../../images/fastai_p1_v3/lesson_1/1.png)

The main thing that hopefully you're going to agree at the end of this is that you can do world-class practitioner level deep learning regardless of who you are. <br>
`끝에 가서 여러분이 동의하기를 바라는 가장 중요한 것은 여러분이 누구와 상관없이 세계적인 수준의 실무자 수준의 깊은 학습을 할 수 있다는 것이다.`

Main places to be looking for things are:
- [course-v3.fast.ai](http://course-v3.fast.ai/)
  - you can find out how to get a GPU and other information.
- [forums](https://forums.fast.ai/latest)

### Who is Jeremy Howard? [[5:27](https://youtu.be/BWWm4AzsdLk?t=327)]

![](../../../../images/fastai_p1_v3/lesson_1/2.png)

A little bit about why we should listen to Jeremy.

### Using machine learning to do useful things [[6:48](https://youtu.be/BWWm4AzsdLk?t=408)]

![](../../../../images/fastai_p1_v3/lesson_1/3.png)

### What can I do after 7 lessons? [[7:25](https://youtu.be/BWWm4AzsdLk?t=446)]

![](../../../../images/fastai_p1_v3/lesson_1/4.png)

There is a lot as to how much people put into this. Jeremy knows a lot of people who work full-time on fast AI. Some folks whose do the two parts can spend a whole year doing it really intensively. Jeremy knows some folks watch the videos on double-speed and never do any homework and come at the end of it with a general sense of what's going on. So, there's lots of different ways you can do this.
`이 일에 얼마나 많은 사람들이 투입하는지에 대해서는 많은 것이 있다. 제레미는 fast AI에 full-time으로 일하는 사람들을 많이 알고 있다. 두 부분을 하는 몇몇 사람들은 그것을 하는데 1년 전체를 쓸 수 있다. 제레미는 어떤 사람들이 비디오를 이중속도로 보고 어떤 숙제도 하지 않고 무슨 일이 일어나고 있는지에 대한 일반적인 감각으로 끝내는 것을 알고 있다. 그래서, 여러분이 이것을 할 수 있는 많은 다양한 방법들이 있다.`

If you follow along with 10 hours a week or so approach for the 7 weeks, by the end, you will be able to:

1. Build an image classification model on pictures that you choose that will work at a world class level.
2. Classify text using whatever datasets you're interested in.
3. Make predictions of commercial applications like sales.
4. Build recommendation systems such as the one used by Netflix.

Not toy examples of any of these but actually things that can come top 10 in Kaggle competitions, that can beat everything that's in the academic community.

The prerequisite is one year of coding and high school math.

### Myths about Deep Learning and AI [[9:05](https://youtu.be/BWWm4AzsdLk?t=545)]

This lesson breaks down the previously held myths about Deep Learning and AI which are no longer true—now, literally anyone with a computer can learn.

![](../../../../images/fastai_p1_v3/lesson_1/5.png)

You will probably hear a lot of naysayers, less now than a couple of years ago than we started. A lot of them telling you that you can't do it or you shouldn't be doing it or that deep learning got all these problems. It's not perfect. These are all things that people claim about, which are either pointless or untrue. <br>
`당신은 아마도 우리가 시작한지 2년도 안된 지금 많은 비관론자들의 말을 들을 것이다. 그들 중 많은 사람들이 여러분이 그것을 할 수 없거나, 그것을 해서는 안 된다거나, deep learning이 이러한 모든 문제들을 가지고 있다고 말한다. 맞지 않는 말입니다. 사람들이 주장하는 모든 것들이 무의미하거나 사실이 아니야.`

- It's not a black box. It's really great for interpreting what's going on. <br>
` 블랙박스가 아니다. 무슨 일이 일어나고 있는지 해석하는 것은 정말 훌륭하다.`
- It does not need much data for most practical applications. <br>
`대부분의 실용적 용도에 많은 데이터가 필요하지 않다.`
- You don't need a PhD. Rachel has one so it doesn't actually stop you from doing deep learning if you have a PhD. <br>
`박사학위는 필요 없다. Rachel이 박사학위를 가지있다고 해서 실제로 여러분이 deep learning을 하는 것을 막지 못한다.`
- It can be used very widely for lots of different applications, not just for vision. <br>
`비전뿐만 아니라 다양한 애플리케이션에 매우 광범위하게 사용할 수 있다.`
- You don't need lots of hardware. 36 cents an hour server is more than enough to get world-class results for most problems. <br>
`하드웨어가 많이 필요하지 않다. 시간당 36센트는 대부분의 문제에서 세계적인 수준의 결과를 얻기에 충분하다.`
- It is true that maybe this is not going to help you build a sentient brain, but that's not our focus. For all the people who say deep learning is not interesting because it's not really AI, not really a conversation that Jeremy interested in. We are focused on solving interesting real-world problems. <br>
` 어쩌면 이것이 지각 있는 뇌를 만드는 데 도움이 되지 않을 수도 있다는 것은 사실이지만, 그것은 우리의 초점은 아니다. deep learning은 진짜 AI가 아니라고 하는 모든 사람들의 대화에 대해서 Jeremy는 사실 관심이 없다. 우리는 흥미로운 현실 문제를 해결하는 데 초점을 맞추고 있다.`

### What are you going to be able to do by the end of lesson 1 [[10:24](https://youtu.be/BWWm4AzsdLk?t=624)]

![](../../../../images/fastai_p1_v3/lesson_1/6.png)

Cricket vs Baseball - an example by Nikhil of what you are going to be able to do by the end of lesson 1.

### Topdown approach [[11:02](https://youtu.be/BWWm4AzsdLk?t=662)]

![You will learn how it works before you learn why it works](../../../../images/fastai_p1_v3/lesson_1/7.png)

**You will learn how it works before you learn why it works.**

We are going to start by looking at code which is different to many of academic courses. We are going to learn to build a useful thing today. That means that at the end of today, you won't know all the theory. There will be lots of aspects of what we do that you don't know why or how it works. That's okay! You will learn why and how it works over the next 7 weeks. But for now, we've found that what works really well is to actually get your hands dirty coding—not focusing on theory. Because, it's still a situation where people who are good practitioners have a really good feel for how to work with code and how to work with data and you can only get that through experience. The best way to get that feel of how to get good models is to create lots of models through lots of coding and study them carefully. So, let's try that, let's try getting started. <br>
`우리는 많은 대학 수업과는 다르게 코드부터 살펴보려고 한다. 우리는 오늘 유용한 것을 만드는 것을 배울 것이다. 그것은 오늘 말미에 당신이 모든 이론을 알 수 없다는 것을 의미한다. 우리가 하는 일에는 왜 그러는지 어떻게 작동하는지 모르는 많은 측면이 있을 것이다. 괜찮다! 7주 동안 왜 그리고 어떻게 작동하는지 알게 될 것이다. 하지만 현재로서는 이론에 초점을 맞추지 않고 실제로 직접 코딩을 하는 것이 효과적이라는 것을 알아냈다. 왜냐하면, 그것은 여전히 훌륭한 실무자인 사람들이 어떻게 코드로 일하는지 그리고 어떻게 데이터를 가지고 일하는지에 대해 정말로 좋은 느낌을 가지고 있는 상황이고 당신은 오직 경험을 통해서만 그것을 얻을 수 있기 때문이다. 좋은 모델을 얻는 방법에 대한 느낌을 얻는 가장 좋은 방법은 많은 코딩을 통해 많은 모델을 만들고 그것들을 주의 깊게 연구하는 것이다. 자, 시작해 봅시다.`

## What's your pet [[12:26](https://youtu.be/BWWm4AzsdLk?t=746)]

Open your Jupyter Notebook and click on [lesson1-pets.ipynb](https://nbviewer.jupyter.org/github/fastai/course-v3/blob/master/nbs/dl1/lesson1-pets.ipynb).

Real deep learning practitioners know the keyboard shortcuts. The keyboard shortcut is:

<kbd>Shift</kbd>+<kbd>Enter</kbd> to run a cell.

We are going to go through this quickly and later on we're going to go back over it more carefully. Here's the quick version to get a sense of what's going on. So, here we are in lesson 1.

These three lines is what we start every notebook with:

```python
%reload_ext autoreload
%autoreload 2
%matplotlib inline
```

These things starting `%` are special directives to Jupyter Notebook itself, they are not Python code. They are called "magics". The details aren't very important but basically it says: <br>
`%를 시작하는 것들은 Jupyter Notebook 자체에 대한 특별한 명령이지 파이선 코드는 아니다. 그들은 "마법들"이라고 불린다. 자세한 내용은 그다지 중요하지 않지만 기본적으로 다음과 같이 말하고 있다.`
- If somebody changes underlying library code while I'm running this, please reload it automatically. <br>
`이 작업을 실행하는 동안 기본 라이브러리 코드를 변경한 경우 자동으로 다시 로드하십시오.`
- If somebody asks to plot something, then please plot it here in this Jupyter Notebook. <br>
`만약 누군가가 뭔가 뭔가를 그리라고 한다면, 여기 Jupyter Notebook에 그것을 그려주십시오.`


[[14:00](https://youtu.be/BWWm4AzsdLk?t=840)] The next two lines load up the fastai library:

```python
from fastai import *
from fastai.vision import *
```

What is fastai library? If you go to [docs.fast.ai](http://docs.fast.ai), this is the fastai library:

![](../../../../images/fastai_p1_v3/lesson_1/fastai_lib.png)

Everything we are going to do is going to be using either fastai or [PyTorch](https://pytorch.org/) which fastai sits on top of. PyTorch is fast growing extremely popular library. It's a bit newer than TensorFlow, so in a lot of ways it's more modern than TensorFlow. We use it because we used to use TensorFlow a couple years ago and we found we can do a lot more, a lot more quickly with PyTorch.

Currently fastai supports four applications: <br>
`현재 fastai는 네 가지 애플리케이션을 지원한다.`

1. Computer vision
2. Natural language text
3. Tabular data
4. Collaborative filtering

[[15:45](https://youtu.be/BWWm4AzsdLk?t=945)]

`import *` - If you are a Python software engineer, you probably feeling sick because this is something you've all been told to never ever do.

There are very good reasons to not use `import *` in standard production code with most libraries. But things like MATLAB is the opposite. Everything is there for you all the time. You don't even have to import things a lot of the time. It's kind of funny - we've got these two extremes of how do I code. The scientific programming community has one way, and then software engineering community has the other. Both have really good reasons for doing things. <br>
`대부분의 라이브러리들이 있는 표준 상용 코드에 'import *' 를 사용하지 않는 데는 그럴 만한 이유가 있다. 그러나 MATLAB와 같은 것들은 정반대다. 모든 것이 너를 위해 항상 있다. 필요한 것들을 많이 import할 필요도 없다. 좀 웃긴데- 어떻게 내가 코딩를 해야 하는지에 대한 두가지 극단적인 방법이 있다. 과학 프로그래밍 커뮤니티에는 한 가지 방법이 있고, 소프트웨어 엔지니어링 커뮤니티에는 다른 방법이 있다. 둘 다 일을 하는 데 정말 좋은 이유가 있다.`

With the fastai library, we actually support both approaches. In Jupyter Notebook where you want to be able to quickly interactively try stuff out, you don't want to constantly going back up to the top and importing more stuff. You want to be able to use lots of tab complete and be very experimental, so `import *` is great. When you are building stuff in production, you can do the normal PEP8 style proper software engineering practices. This is a different style of coding. It's not that there are no rules in data science programming, the rules are different. When you're training models, the most important thing is to be able to interactively experiment quickly. So you will see we use a lot of different processes, styles, and stuff to what you are used to. But they are there for a reason and you'll learn about them over time. <br>
`Fastai 라이브러리를 통해 우리는 실제로 두 가지 접근 방식을 모두 지원한다. 빨리 대화식으로 시험해 보고 싶은 Jupyter Notebook에서는, 끊임없이 위로 올라가서 더 필요한 것들을 import하고 싶어 하지 않는다. 탭 완료를 많이 사용할 수 있고 매우 실험적이기를 원하기 때문에 'import *'는 훌륭하다. 당신이 상용 제품을 만들 때, 당신은 일반적인 PEP8 스타일의 적절한 소프트웨어 엔지니어링 관행을 할 수 있다. 이것은 다른 스타일의 코딩이다. 데이터 과학 프로그래밍에 규칙이 없다는 것이 아니라 규칙이 다르다는 겁니다. 모델을 훈련할 때, 가장 중요한 것은 빠르게 상호작용적으로 실험할 수 있는 것이다. 그래서 우리는 여러분이 익숙한 것에 많은 다른 프로세스, 스타일, 그리고 그런 것들을 사용하는 것을 볼 수 있을 겁니다. 하지만 그들은 이유가 있어서 그곳에 있고 당신은 시간이 지남에 따라 그것에 대해 알게 될 것이다.`

The other thing to mention is that the fastai library is designed in a very interesting modular way and when you do use `import *`, there's far less clobbering of things than you might expect. It's all explicitly designed to allow you to pull in things and use them quickly without having problems. <br>
`또 하나 언급해야 할 것은 이 FastAI 라이브러리에는 매우 흥미로운 모듈 방식으로 설계되어 있으며, 'import *'를 사용할 때 여러분이 예상하는 것보다 잡동사니들이 훨씬 적다는 점이다. 이 모든 것은 여러분이 문제를 일으키지 않고 빠르게 물건을 끌어다 쓸 수 있도록 명시적으로 고안된 것이다.`

## Looking at the data [[17:56](https://youtu.be/BWWm4AzsdLk?t=1076)]

Two main places that we will be tending to get data from for the course: <br>
`본 코스의 데이터를 얻기 위한 2가지 주요 장소:`

1. Academic datasets <br>
`1. 학술 데이터 세트`
    - Academic datasets are really important. They are really interesting. They are things where academics spend a lot of time curating and gathering a dataset so that they can show how well different kinds of approaches work with that data. The idea is they try to design datasets that are challenging in some way and require some kind of breakthrough to do them well. <br>
    `학술 데이터 세트는 정말 중요하다. 그것들은 정말 흥미롭다. 이러한 것들은 학자들이 데이터셋을 조정하고 수집하는 데 많은 시간을 할애하여 서로 다른 종류의 접근방식이 그 데이터에 얼마나 잘 작용하는지 보여줄 수 있도록 하는 것이다. 그 아이디어는 그들이 어떤 면에서 도전적인 데이터셋을 설계하려고 하고 그것을 잘 하기 위해 어떤 종류의 돌파구가 필요한 데이터셋을 설계하려고 노력한다는 것이다.`
    - We are going to start with an academic dataset called the pet dataset. <br>
    `우리는 애완동물 데이터셋이라고 불리는 학문적 데이터셋으로 시작할 것이다.`
2. Kaggle competition datasets
`2. Kaggle competition 데이터 세트`

Both types of datasets are interesting for us particularly because they provide strong baseline. That is to say you want to know if you are doing a good job. So with Kaggle datasets that come from a competition, you can actually submit your results to Kaggle and see how well you would have gone in that competition. If you can get in about the top 10%, then I'd say you are doing pretty well. <br>
`두 종류의 데이터셋은 특히 강력한 기준선을 제공하기 때문에 우리에게 흥미롭다. 즉 일을 잘 하고 있는지 알고 싶다는 것이다. 따라서 competition에서 얻은 Kaggle 데이터 세트를 사용하여 실제로 결과를 Kaggle에 제출하고 해당 경쟁에서 얼마나 잘 나갔는지 확인할 수 있다. 만약 당신이 상위 10%에 들어갈 수 있다면, 나는 당신이 꽤 잘 하고 있다고 말할 것이다.`


Academic datasets, academics write down in papers what the state of the art is so how well did they go with using models on that dataset. So this is what we are going to do. We are going to try to create models that get right up towards the top of Kaggle competitions, preferably in the top 10, not just top 10% or that meet or exceed academic state-of-the-art published results. So when you use an academic dataset, it's important to cite it. Here there's a link to the [Oxford-IIIT Pet Dataset paper](http://www.robots.ox.ac.uk/~vgg/publications/2012/parkhi12a/parkhi12a.pdf) that it's from. You don't need to read that paper right now, but if you are interested in learning more about it and why it was created and how it was created, all the details are there. <br>
`학술 데이터셋, 학자들은 그 데이터셋에 모델을 얼마나 잘 사용했는지를 논문에서 기록한다. 이것이 우리가 할 일 입니다. 우리는 카글 대회, 특히 상위 10%가 아니라 상위 10위 안에 들거나 학술 최신 발표 결과를 충족시키거나 초과하는 모델을 만들 계획이다. 따라서 학술 자료 세트를 사용할 때는 인용하는 것이 중요하다. 여기 그것이 보낸 [Oxford-IIIT Pet Dataset paper](http://www.robots.ox.ac.uk/~vgg/publications/2012/parkhi12a/parkhi12a.pdf)의 링크가 있다. 지금 당장 그 논문을 읽을 필요는 없지만, 그 논문에 대해 좀 더 자세히 알고, 왜 그것이 만들어졌고, 어떻게 만들어졌는지에 관심이 있다면, 모든 세부 사항은 거기에 있다.`

In this case, this is a pretty difficult challenge. The Pet dataset is going to ask us to distinguish between 37 different categories of dog breed and cat breed. So that's really hard. In fact, every course until this one, we've used a different dataset which is one where you just have to decide if something is a dog or a cat. So you've got a 50-50 chance right away and dogs and cats look really different. Or else lots of dog breeds and cat breeds look pretty much the same. <br>
`이 경우, 이것은 꽤 어려운 도전이다. 펫 데이터 세트는 우리에게 37개의 다른 종류의 개 품종과 고양이 품종을 구별할 것을 요구할 것이다. 그래서 그것은 정말 어렵다. 사실, 이 과정까지 우리는 다른 데이터 세트를 사용했는데, 이 데이터 세트는 어떤 것이 개인지, 아니면 고양이인지 결정해야 하는 데이터 세트였습니다. 50대 50의 확률로 개와 고양이는 정말 다르게 보인다. 아니면 많은 개 품종들과 고양이 품종들이 거의 똑같이 보인다.`

So why have we changed the dataset? We've got to the point now where deep learning is so fast and so easy that the dogs versus cats problem which a few years ago was considered extremely difficult around 80% accuracy was the state of the art, it's now too easy. Our models were basically getting everything right all the time without any tuning and so there weren't really a lot of opportunities for me to show you how to do more sophisticated stuff. So we've picked a harder problem this year. <br>
`그럼 왜 데이터 세트를 변경한 겁니까? 우리는 이제 깊이 있는 학습이 너무 빠르고 쉬워서 몇 년 전에 80%정확도 정도로 매우 어렵다고 여겨졌던 개 대 고양이 문제가 예술의 상태였고, 지금은 너무 쉽다. 저희 모델은 기본적으로 튜닝 없이 항상 모든 것을 제대로 해내고 있었고 그래서 여러분께 좀 더 정교한 것을 보여드릴 기회가 별로 없었답니다. 그래서 우리는 올해 더 어려운 문제를 골랐다.`

[[20:51](https://youtu.be/BWWm4AzsdLk?t=1251)]

This kind of thing where you have to distinguish between similar categories is called **fine grained classification** in the academic context. <br>
`이와 유사한 범주를 구분해야 하는 이런 종류의 것을 학문적 맥락에서 **fine grained 분류**라고 한다.`

### `untar_data`

The first thing we have to do is download and extract the data that we want. We're going to be using this function called `untar_data` which will download it automatically and untar it. AWS has been kind enough to give us lots of space and bandwidth for these datasets so they'll download super quickly for you. <br>
`우리가 가장 먼저 해야 할 일은 우리가 원하는 데이터를 다운로드하고 압축해제하는 것이다. untar_data라는 이 기능을 이용해 자동 다운로드하고 untar 할 겁니다. AWS는 이러한 데이터셋을 위한 많은 공간과 대역폭을 제공하므로, 그들이 당신을 위해 매우 빠르게 다운로드될 것이다.`

```python
path = untar_data(URLs.PETS); path
```

### `help`

The first question then would be how do I know what `untar_data` does. You could just type help and you will find out what module it came from (since we did `import *` you don't necessarily know that), what it does, and something you might not have seen before even if you are an experienced programmer is what exactly you pass to it. You're probably used to seeing the names: url, fname, dest, but you might not be used to seeing `Union[pathlib.Path, str]`. These bits are types and if you're used to typed programming language, you would be used to seeing them, but Python programmers are less used to it. But if you think about it, you don't actually know how to use a function unless you know what type each thing is that you're providing it. So we make sure that we give you that type information directly here in the help. <br>
`그렇다면 첫 번째 질문은 'untar_data'가 무엇을 하는지 어떻게 알 것인가 하는 것이다. 당신은 단지 'help'를 타이핑하면 그것이 어떤 모듈에서 왔는지 알게 될 것이다. 당신은 아마도 url, fname, dest, 라는 이름들을 보는 데 익숙하겠지만, 'Union[pathlib.Path, str]'을 보는 데는 익숙하지 않을지도 모른다." 이런 비트들은 type이고 type형 프로그래밍 언어에 익숙하다면 보는 데 익숙하겠지만 Python 프로그래머들은 덜 익숙하다. 그러나 생각해 보면, 각각의 것이 어떤 유형인지, 즉 어떤 기능을 제공하는지를 알지 못하면 실제로 그 기능을 어떻게 사용하는지 알 수 없다. 그래서 우리는 여러분에게 이런 유형의 정보를 바로 여기 도움에 줄 수 있도록 한다.`

In this case, `url` is a string, `fname` is either path or a string and defaults to nothing (`Union` means "either"). `dest` is either a string or a path and defaults to nothing. <br>
`이 경우 url은 문자열이고 fname은 경로 또는 문자열이며 기본값은 없다.('Union'은 둘 중에 하나를 의미) 'dest'는 문자열이나 경로로 기본값은 없는 것으로 되어 있다.`

```python
help(untar_data)

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
Help on function untar_data in module fastai.datasets:

untar_data(url:str, fname:Union[pathlib.Path, str]=None, dest:Union[pathlib.Path, str]=None)
    Download `url` if doesn't exist to `fname` and un-tgz to folder `dest`
```

We'll learn more shortly about how to get more documentation about the details of this, but for now, we can see we don't have to pass in a file name `fname` or a destination `dest`, it'll figure them out for us from the URL. <br>
`자세한 내용은 잠시 후 자세히 알아보겠지만, 현재로서는 파일 이름이나 목적지 'dest'를 입력할 필요가 없다는 것을 알 수 있으며, URL에서 확인할 수 있을 것이다.`

For all the datasets we'll be using in the course, we already have constants defined for all of them (i.e: `URLs.PETS`). So in this [URLs](https://github.com/fastai/fastai/blob/master/fastai/datasets.py) class, you can see where it's going to grab it from. <br>
`본 코스에서 사용할 모든 데이터 세트에 대해 이미 모든 데이터에 대해 정의된 상수가 있다(예: 'URLs'.PETS). [URLs](https://github.com/fastai/fastai/blob/master/fastai/datasets.py) class 에서, 이것들을 볼 수 있다.

`untar_data` will download that to some convenient path and untar it for us and it will then return the value of path.

```python
path = untar_data(URLs.PETS); path

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet')
```

In Jupyter Notebook, you can just write a variable on its own (semicolon is just an end of statement in Python) and it prints it. You can also say `print(path)` but again, we are trying to do everything fast and interactively, so just write it and here is the path where it's given us our data. <br>
`Jupyter Notebook에서는 변수를 그 자체만으로 쓸 수 있다(세미콜론은 python에서 문장의 끝을 의미한다). 그리고 그것을 print한다. 'print(path)'라고 말할 수도 있지만, 다시 말해 우리는 모든 것을 빠르고 상호적으로 하려고 노력하고 있으니, 그냥 작성하고 이것이 우리의 데이터를 담고 있는 경로이다.`

Next time you run this, since you've already downloaded it, it won't download it again. Since you've already untared it, it won't untar it again. So everything is designed to be pretty automatic and easy. <br>
`다음에 이걸 실행하면, 이미 다운받았기 때문에, 다시 다운로드를 하지 않는다. 여러분이 이미 압축을 해제 했으니, 그것은 다시 압축해제하지 않을 것이다. 그래서 모든 것은 꽤 자동적이고 쉽게 설계되어 있다.`

[[23:50](https://youtu.be/BWWm4AzsdLk?t=1430)]

There are some things in Python that are less convenient for interactive use than they should be. For example, when you do have a path object, seeing what's in it actually takes a lot more typing than I would like. So sometimes we add functionality into existing Python stuff. One of the things we do is add a `ls()` method to path. <br>
`Python에는 대화형 사용이 필요 이상으로 편리하지 않은 것들이 있다. 예를 들어, 여러분이 경로 객체를 가지고 있을 때, 그 안에 있는 것을 보는 것은 실제로 내가 원하는 것보다 훨씬 더 많은 타이핑을 필요로 한다. 그래서 때때로 우리는 기존의 python 물건에 기능성을 추가한다. 우리가 하는 일 중 하나는 'ls()' 를 path에 추가하는 것이다.`

```python
path.ls()

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
['annotations', 'images']
```

These are what's inside this path, so that's what we just downloaded.
`방금 우리가 다운로드한 것들이 이 경로 안에 있다.`

### Python 3 pathlib [[24:25](https://youtu.be/BWWm4AzsdLk?t=1465)]

```python
path_anno = path/'annotations'
path_img = path/'images'
```

If you are an experienced Python programmer, you may not be familiar with this approach of using a slash like this. This is a really convenient function that's part of Python 3. It's functionality from [pathlib](https://docs.python.org/3/library/pathlib.html). Path object is much better to use than strings. They let you use basically create sub paths like this. It doesn't matter if you're on Windows, Linux, or Mac. It is always going to work exactly the same way. `path_img` is the path to the images in that dataset.
`만약 당신이 경험이 풍부한 파이썬 프로그래머라면, 당신은 이런 슬래시를 사용하는 이 접근법에 익숙하지 않을 것이다. 이것은 파이톤 3의 일부분인 정말 편리한 기능이다. 그것은 [pathlib](https://docs.python.org/3/library/pathlib.html).에서 제공하는 기능이다. Path 객체가 문자열보다 훨씬 낫다. 이렇게 기본적으로 하위 경로를 만들 수 있는 겁니다. 당신이 Windows, Linux, Mac에 있든 상관없다. 그것은 항상 정확히 같은 방식으로 작동될 것이다. path_img는 해당 데이터 세트에 있는 이미지의 경로다.`

[[24:57](https://youtu.be/BWWm4AzsdLk?t=1497)]

So if you are starting with a brand new dataset trying to do some deep learning on it. What do you do? Well, the first thing you would want to do is probably see what's in there. So we found that `annotations` and `images` are the directories in there, so what's in this images?

### `get_image_files` [[25:15](https://youtu.be/BWWm4AzsdLk?t=1515)]

There's a lot of functions in fastai for you. There's one called `get_image_files` that will just grab an array of all of the image files based on extension in a path.

```python
fnames = get_image_files(path_img)
fnames[:5]

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
[PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/american_bulldog_146.jpg'),
 PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/german_shorthaired_137.jpg'),
 PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/japanese_chin_139.jpg'),
 PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/great_pyrenees_121.jpg'),
 PosixPath('/data1/jhoward/git/course-v3/nbs/dl1/data/oxford-iiit-pet/images/Bombay_151.jpg')]
```

 This is a pretty common way for computer vision datasets to get passed around - just one folder with a whole bunch of files in it. So the interesting bit then is how do we get the labels. In machine learning, the labels refer to the thing we are trying to predict. If we just eyeball this, we could immediately see that the labels are actually part of the file names. It's kind of like `path/label_number.extension`. We need to somehow get a list of `label` bits of each file name, and that will give us our labels. Because that's all you need to build a deep learning model:
 - Pictures (files containing the images)
 - Labels

In fastai, this is made really easy. There is an object called `ImageDataBunch`. An `ImageDataBunch` represents all of the data you need to build a model and there's some factory methods which try to make it really easy for you to create that DataBunch - a training set, a validation set with images and labels.

In this case, we need to extract the labels from the names. We are going to use `from_name_re`. `re` is the module in Python that does regular expressions - things that's really useful for extracting text.

Here is the regular expression that extract the label for this dataset:

```python
np.random.seed(2)
pat = r'/([^/]+)_\d+.jpg$'
```

**Regular expressions** or in short regex is a way to search a string in text using pattern matching methods.

Let's deconstruct this regex pattern, `/([^/]+)_\d+.jpg$` by reading it backwards:

| Expression      | Explaination                                                             |
| --------------- |:-------------------------------------------------------------------------|
| `$`             | end of search                                                            |
| `.jpg`          | last chars to be found in search string, also right file format checking |
| `\d`            | numerical digits, `+` sign denotes can be one or more of them            |
| `_`             | should come before start of digits                                       |
| `()`            | denotes group of characters                                              |
| `[]`            | denotes another subgroup if characters in previous group                 |
| `^/`            | `^` denotes negation , so `+` says all other chars except `/`            |
| `( [ ^/ ] + )`  | searches all characters except `/`                                       |
| `/`             | first `/` in regex says, end of search                                   |

Considering search string was `PosixPath('images/japanese_chin_139.jpg')`, this regex pattern will give us string `japanese_chin`.

With this factory method, we can basically say:
- `path_img`: a path containing images
- `fnames`: a list of file names
- `pat`: a regular expression (i.e. pattern) to be used to extract the label from the file name
- `ds_tfms`: we'll talk about transforms later
- `size`: what size images do you want to work with.

That might seem weird because images have size. This is a shortcoming of current deep learning technology which is that a GPU has to apply the exact same instruction to a whole bunch of things at the same time in order to be fast. If the images are different shapes and sizes, you can't do that. So we actually have to make all of the images the same shape and size. In part 1 of the course, we are always going to be making images square shapes. Part 2, we will learn how to use rectangles as well. It turns out to be surprisingly nuanced. But pretty much everybody in pretty much all computer vision modeling nearly all of it uses this approach of square. 224 by 224, for reasons we'll learn about, is an extremely common size that most models tend to use so if you just use `size=224`, you're probably going to get pretty good results most of the time. This is kind of the little bits of artisanship that I want to teach you which is what generally just works. So if you just use size 224, that'll generally just work for most things most of the time.

```python
data = ImageDataBunch.from_name_re(path_img, fnames, pat, ds_tfms=get_transforms(), size=224)
data.normalize(imagenet_stats)
```

[[29:16](https://youtu.be/BWWm4AzsdLk?t=1756)]

`ImageDataBunch.from_name_re` is going to return a DataBunch object. In fastai, everything you model with is going to be a DataBunch object. Basically DataBunch object contains 2 or 3 datasets - it contains your training data, validation data, and optionally test data. For each of those, it contains your images and your labels, your texts and your labels, or your tabular data and your labels, or so forth. And that all sits there in this one place (i.e. `data`).

Something we will learn more about in a little bit is normalization. But generally in nearly all machine learning tasks, you have to make all of your data about the same "size" - they are specifically about the same mean and standard deviation. So there is a normalize function that we can use to normalize our DataBunch in that way.

[[30:25](https://youtu.be/BWWm4AzsdLk?t=1825)]

**Question**:question:: What does the function do if the image size is not 224?

This is what we are going to learn about shortly. Basically this thing called transforms (i.e. `ds_tfms=get_transforms()`) is used to do a number of the things and one of the things it does is to make something size 224.

### `data.show_batch`

Let's take a look at a few pictures. Here are a few pictures of things from my DataBunch. So you can see data.show_batch can be used to show me some of the contents in my DataBunch. So you can see roughly what's happened is that they all seem to have being zoomed and cropped in a reasonably nice way. So basically what it'll do is something called by default center cropping which means it'll grab the middle bit and it'll also resize it. We'll talk more about the detail of this because it turns out to actually be quite important, but basically a combination of cropping and resizing is used.

```python
data.show_batch(rows=3, figsize=(7,6))
```

![](../../../../images/fastai_p1_v3/lesson_1/8.png)

Something else we are going to learn about is we also use this to do something called data augmentation. So there's actually some randomization in how much and where it crops and stuff like that.

Basic the basic idea is some cropping, resizing, and padding. So there's all kinds of different ways it depends on data augmentation which we are going to learn about shortly.

[[31:51](https://youtu.be/BWWm4AzsdLk?t=1911)]
**Question**:question:: What does it mean to normalize the images?

Normalizing the images, we're going to be learning more about later in the course, but in short, it means that the pixel values start out from naught (0) to 255. And some channels might tend to be really bright, some might tend to be really not bright at all, some might vary a lot, and some might not very much at all. It really helps train a deep learning model if each one of those red green and blue channels has a mean of zero and a standard deviation of one.

If your data is not normalized, it can be quite difficult for your model to train well. So if you have trouble training a model, one thing to check is that you've normalized it.

[[33:00](https://youtu.be/BWWm4AzsdLk?t=1980)]
**Question**:question:: As GPU mem will be in power of 2, doesn't size 256 sound more practical considering GPU utilization compared to 224?

The brief answer is that the models are designed so that the final layer is of size 7 by 7, so we actually want something where if you go 7 times 2 a bunch of times (224 = 7*2*2*2*2*2), then you end up with something that's a good size.

[[33:27](https://youtu.be/BWWm4AzsdLk?t=2007)]

We will get to all these details but the key thing is I wanted to get to training a model as quickly as possible.

### It is important to look at the data

One of the most important thing to be a really good practitioner is to be able to look at your data. So it's really important to remember to go `data.show_batch` and take a look. It's surprising how often when you actually look at the dataset you've been given that you realize it's got weird black borders on it, some of the things have text covering up some of it, or some of it is rotated in odd ways. So make sure you take a look.

The other thing we want to do at is to look at the labels. All of the possible label names are called your classes. With DataBunch, you can print out your `data.classes`.

```python
print(data.classes)
len(data.classes),data.c

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
['american_bulldog', 'german_shorthaired', 'japanese_chin', 'great_pyrenees', 'Bombay', 'Bengal', 'keeshond', 'shiba_inu', 'Sphynx', 'boxer', 'english_cocker_spaniel', 'american_pit_bull_terrier', 'Birman', 'basset_hound', 'British_Shorthair', 'leonberger', 'Abyssinian', 'wheaten_terrier', 'scottish_terrier', 'Maine_Coon', 'saint_bernard', 'newfoundland', 'yorkshire_terrier', 'Persian', 'havanese', 'pug', 'miniature_pinscher', 'Russian_Blue', 'staffordshire_bull_terrier', 'beagle', 'Siamese', 'samoyed', 'chihuahua', 'Egyptian_Mau', 'Ragdoll', 'pomeranian', 'english_setter']

(37, 37)
```

 That's all of the possible labels that we found by using that regular expression on the file names. We learnt earlier on at the top that there are 37 possible categories, so just checking `len(data.classes)`, it is indeed 37. DataBunch will always have a property called `c`. We will get to the technical detail later, but for now, you can kind of think of it as being the number of classes. For things like regression problems and multi-label classification, that's not exactly accurate, but it'll do for now. It is important to know that `data.c` is a really important piece of information that is something like, or at least for classification problems it is, the number of classes.

 ## Training [[35:07](https://youtu.be/BWWm4AzsdLk?t=2107)]

 Believe it or not, we are now ready to train a model. A model is trained in fastai using something called a "learner".

 - **DataBunch**: A general fastai concept for your data, and from there, there are subclasses for particular applications like `ImageDataBunch`.
 - **Learner**: A general concept for things that can learn to fit a model. From that, there are various subclasses to make things easier in particular, there is a `ConvLearner` which is something that will create a convolutional neural network for you.

:loudspeaker: _2018-10-29: there's been one change to fastai v1.0.15 and above—`ConvLearner` is now called `create_cnn`. You'll need to make that change in any notebooks that you've created too. Reference: [forum: lesson 1 official resources and updates](https://forums.fast.ai/t/lesson-1-official-resources-and-updates/27936/7?u=cedric)_

```python
learn = create_cnn(data, models.resnet34, metrics=error_rate)
```

For now, just know that to create a learner for a convolutional neural network, you just have to tell it two things:
- `data`: What's your data. Not surprisingly, it takes a DataBunch.
- `arch`: What's your architecture. There are lots of different ways of constructing a convolutional neural network.

For now, the most important thing for you to know is that there's a particular kind of model called ResNet which works extremely well nearly all the time. For a while, at least, you really only need to be doing choosing between two things which is what size ResNet do you want. There are ResNet34 and ResNet50. When we are getting started with something, I'll pick a smaller one because it'll train faster. That's as much as you need to know to be a pretty good practitioner about architecture for now which is that there are two variants of one architecture that work pretty well: ResNet34 and ResNet50. Start with a smaller one and see if it's good enough.

That is all the information we need to create a convolutional neural network learner.

There is one other thing I'm going to give it though which is a list of metrics. Metrics are literally just things that gets printed out as it's training. So I'm saying I would like you to print out error rate.

[[37:25](https://youtu.be/BWWm4AzsdLk?t=2245)]

![](../../../../images/fastai_p1_v3/lesson_1/c1.png)

The first time I run this on a newly installed box, it downloads the ResNet34 pre-trained weights. What that means is that this particular model has actually already been trained for a particular task. And that particular task is that it was trained on looking at about one and a half million pictures of all kinds of different things, a thousand categories of things, using an image dataset called ImageNet. So we can download those pre-trained weights so that we don't start with a model that knows nothing about anything, but we actually start with a model that knows how to recognize a thousand categories of things in ImageNet. I don't think all of these 37 categories of pet are in ImageNet but there were certainly some kinds of dog and some kinds of cat. So this pre-trained model knows quite a little bit about what pets look like, and it certainly knows quite a lot about what animals look like and what photos look like. So the idea is that we don't start with a model that knows nothing at all, but we start by downloading a model that knows something about recognizing images already. So it downloads for us automatically, the first time we use it, a pre-trained model and then from now on, it won't need to download it again - it'll just use the one we've got.

## Transfer learning [[38:54](https://youtu.be/BWWm4AzsdLk?t=2334)]

:exclamation::exclamation::exclamation: This is really important. We are going to learn a lot about this. It's kind of the focus of the whole course which is how to do this thing called "transfer learning."

How to take a model that already knows how to do something pretty well and make it so that it can do your thing really well. We will take a pre-trained model, and then we fit it so that instead of predicting a thousand categories of ImageNet with ImageNet data, it predicts the 37 categories of pets using your pet data. By doing this, you can train models in 1/100 or less of the time of regular model training with 1/100 or less of the data of regular model training. Potentially, many thousands of times less. Remember I showed you the slide of Nikhil's lesson 1 project from last year? He used 30 images. There are not cricket and baseball images in ImageNet but it turns out that ImageNet is already so good at recognizing things in the world that just 30 examples of people playing baseball and cricket was enough to build a nearly perfect classifier.

## Overfitting [[40:05](https://youtu.be/BWWm4AzsdLk?t=2405)]

Wait a minute, how do you know it can actually recognize pictures of people playing cricket versus baseball in general? Maybe it just learnt to recognize those 30. Maybe it's just cheating. That's called "overfitting". We'll be talking a lot about that during this course. But overfitting is where you don't learn to recognize pictures of say cricket versus baseball, but just these particular cricketers in these particular photos and these particular baseball players in these particular photos. We have to make sure that we don't overfit. The way to do that is using something called a validation set. A validation set is a set of images that your model does not get to look at. So these metrics (e.g. error_rate) get printed out automatically using the validation set - a set of images that our model never got to see. When we created our DataBunch, it automatically created a validation set for us. We'll learn lots of ways of creating and using validation sets, but because we're trying to bake in all of the best practices, we actually make it nearly impossible for you not to use a validation set. Because if you're not using a validation set, you don't know if you're overfitting. So we always print out the metrics on a validation, we've always hold it out, we always make sure that the model doesn't touch it. That's all done for you, and all built into this DataBunch object.
<br>`잠깐만, 그게 실제로 크리켓 대 야구 경기를 하는 사람들의 사진을 알아볼 수 있는지 어떻게 알아? 아마 그 30명을 알아보는 법을 배웠을 거야. 그냥 속임수일 수도 있어. 그것은 "overfitting" 이라고 불린다. 우리는 이 과정 동안 그것에 대해 많은 이야기를 할 것이다. 하지만 overfitting은 여러분이 크리켓 대 야구의 사진을 인식하는 것을 배우지 못하는 곳이지만, 이 사진 속의 특정 크리켓 선수들과 이 특정 사진 속의 특정 야구선수들만을 인식하는 곳이다. 우리는 우리가 너무 잘 맞지 않도록 확실히 해야 한다. 그렇게 하는 방법은 검증 세트라고 불리는 것을 사용하는 것이다. 검증 세트는 모델이 볼 수 없는 이미지 세트입니다. 따라서 이러한 메트릭스(예: error_rate)는 모델에서 볼 수 없었던 일련의 이미지인 검증 세트를 사용하여 자동으로 출력된다. DataBunch를 만들 때 자동으로 검증 세트가 생성됨 우리는 검증 세트를 만들고 사용하는 많은 방법을 배우겠지만, 우리가 모든 모범 사례를 구우려고 하기 때문에, 우리는 실제로 당신이 검증 세트를 사용하지 않는 것을 거의 불가능하게 만든다. 왜냐하면 유효성검사 세트를 사용하고 있지 않다면, 너무 잘 맞는지 모르기 때문이다. 그래서 우리는 항상 검증에 관한 지표를 출력하고, 항상 그것을 내밀고, 항상 모델이 그것에 닿지 않도록 한다. 이 모든 것이 당신을 위해 이루어졌고, 이 모든 것이 이 DataBunch 객체에 내장되어 있다.`

## Fitting your model [[41:40](https://youtu.be/BWWm4AzsdLk?t=2500)]

So now we have a ConvLearner, we can fit it. You can just use a method called `fit` but in practice, you should nearly always use a method called `fit_one_cycle`. In short, one cycle learning is [a paper](https://arxiv.org/abs/1803.09820) that was released in Mar 2018 and turned out to be dramatically better both more accurate and faster than any previous approach. Again, I don't want to teach you how to do 2017 deep learning. In 2018, the best way to fit models is to use something called one cycle.
<br>`이제 ConvLearner가 생겼어. 우린 그걸 fit할 수 있다. 단지 'fit'이라는 방법을 사용할 수 있지만 실제로는 거의 항상 'fit_one_cycle'이라는 방법을 사용해야 한다. 간단히 말해서, one cycle 학습은 [a paper](https://arxiv.org/abs/1803.09820)]로, 2018년 3월에 출시되었으며 이전의 어떤 접근법보다 정확하고 빠른 것으로 판명되었다. 다시 말하지만, 2017년 심오한 학문을 어떻게 하는지 가르쳐 주고 싶지 않다. 2018년에 모형을 맞추는 가장 좋은 방법은 하나의 사이클이라고 불리는 것을 사용하는 것이다.`

For now, just know that this number, `4`, basically decides how many times do we go through the entire dataset, how many times do we show the dataset to the model so that it can learn from it. Each time it sees a picture, it's going to get a little bit better. But it's going to take time and it means it could overfit. If it sees the same picture too many times, it will just learn to recognize that picture, not pets in general. We'll learn all about how to tune this number during the next couple of lessons but starting out with 4 is a pretty good start just to see how it goes and you can actually see after four epochs or four cycles, we got an error rate of 6%. And it took 1 minute and 56 seconds.
<br>`일단은 이 숫자, 4는 기본적으로 전체 데이터셋을 몇 번이고, 몇 번을 모델에 표시하여 데이터셋을 학습할 수 있도록 하는지를 결정한다는 것만 알아두십시오. 사진을 볼 때마다 조금씩 나아질 겁니다. 하지만 그것은 시간이 걸릴 것이고 그것은 그것이 지나치게 적합할 수 있다는 것을 의미한다. 만약 그들이 같은 사진을 너무 많이 본다면, 그것은 단지 일반적으로 애완동물이 아니라 그 사진을 인식하는 것을 배울 것이다. 우리는 이 숫자를 어떻게 조율해야 하는지에 대해 다음 몇 가지 레슨 동안 배우겠지만, 4로 시작하는 것은 그것이 어떻게 진행되는지 보기만 해도 꽤 좋은 시작이고, 실제로 4 에폭이나 4 사이클 후에 우리는 6%의 오류율을 얻었다. 그리고 1분 56초가 걸렸다.`


```python
learn.fit_one_cycle(4)

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
Total time: 01:10
epoch  train loss  valid loss  error_rate
1      1.175709    0.318438    0.099800    (00:18)
2      0.492309    0.229078    0.075183    (00:17)
3      0.336315    0.211106    0.067199    (00:17)
4      0.233666    0.191813    0.057219    (00:17)
```

So 94% of the time, we correctly picked the exact right one of those 94 dog and cat breeds which feels pretty good to me.
<br>`그래서 94%의 시간동안, 우리는 94종의 개와 고양이 품종 중 저에게 꽤 좋은 것을 정확히 골랐다.`

[[44:29](https://youtu.be/BWWm4AzsdLk?t=2669)] But to get a sense of how good it is, maybe we should go back and look at the paper.

![](../../../../images/fastai_p1_v3/lesson_1/oxford_iiit_pets_paper.png)

Remember, I said the nice thing about using academic papers or Kaggle dataset is we can compare our solution to whatever the best people in Kaggle did or in the academics did. This particular dataset of pet breeds is from 2012 and if I scroll through the paper, you'll generally find in any academic paper there'll be a section called experiments about 2/3 of the way through. If you find a section on experiments, then you can find a section on accuracy and they've got lots of different models and their models. The models as you'll read about in the paper, it's really pet specific. They learn something about how pet heads look and how pet bodies look, and pet image in general look. And they combine them all together and once they use all of this complex code and math, they got an accuracy of 59%. So in 2012, this highly pet specific analysis got an accuracy of 59%. These were the top researchers from Oxford University. Today in 2018, with basically about three lines of code, we got 94% (i.e. 6% error). So that gives you a sense of how far we've come with deep learning, and particularly with PyTorch and fastai, how easy things are.
<br>`기억해라, 학술 논문이나 카글 데이터셋을 사용할 때 좋은 점은 우리가 우리의 솔루션을 Kaggle의 최고의 사람들이 했던 것 또는 학계에서 했던 것들과 비교할 수 있다는 것이다. 이 애완견 품종의 특별한 데이터 세트는 2012년에 나온 것이고, 만약 내가 이 논문을 스크롤하면, 여러분은 일반적으로 어떤 학술 논문에서든지 약 2/3의 실험이라고 불리는 부분이 있을 겁니다. 만약 여러분이 실험에 관한 섹션을 발견한다면, 여러분은 정확성에 관한 섹션을 찾을 수 있을 것이고, 그들은 많은 다른 모델들과 그들의 모델들을 가지고 있다. 여러분이 논문에서 읽게 될 모델들은 정말 특별하다. 그들은 애완동물의 머리가 어떻게 생겼는지, 그리고 어떻게 생겼는지, 그리고 일반적으로 애완동물 이미지에 대해 배운다. 그리고 이 모든 것을 합쳐서 일단 이 복잡한 코드와 수학을 다 쓰면 59%의 정확도를 얻게 되는 겁니다. 그래서 2012년에 이 애완 동물들의 특정한 분석은 59%의 정확도를 얻었다. 이들은 옥스퍼드 대학의 최고 연구원들이다. 2018년 오늘 기본적으로 3줄 정도의 코드를 가지고 94%(즉, 6%의 오차)를 얻었다. 그래서 우리가 얼마나 deep learning을 해왔는지, 특히 PyTorch와 Fastai의 경우, 일이 얼마나 쉬운지를 알 수 있다.`

[[46:43](https://youtu.be/BWWm4AzsdLk?t=2803)]
We just trained a model. We don't know exactly what that involved or how it happened but we do know that with 3 or 4 lines of code, we've built something which smashed the accuracy of the state-of-the-art of 2012. 6% error certainly sounds like pretty impressive for something that can recognize different dog breeds and cat breeds, but we don't really know why it works, but we will. That's okay.
<br>`우리는 방금 모델을 훈련시켰다. 우리는 정확히 무슨 일이 일어났는지 또는 어떻게 일어났는지 모르지만, 우리는 코드 3-4줄로 2012년의 최첨단 기술의 정확성을 무너뜨리는 무언가를 구축했다는 것을 알고 있다. 6%의 실수는 확실히 다른 개 품종과 고양이 품종을 인식할 수 있는 것에 대해 꽤 인상적으로 들리지만, 우리는 그것이 왜 효과가 있는지 잘 모르지만, 우리는 그렇게 할 것이다. 좋습니다.`

### Getting the most out of this course

The number one regret of past students:

![](../../../../images/fastai_p1_v3/lesson_1/102.png)

> :exclamation::exclamation::exclamation: **So please run the code. Really run the code.** :exclamation::exclamation::exclamation: [[47:54](https://youtu.be/BWWm4AzsdLk?t=2874)]

Your most important skills to practice are learning and understanding what goes in and what comes out.

![](../../../../images/fastai_p1_v3/lesson_1/103.png)

Fastai library is pretty new, but it's getting an extraordinary amount of traction. It's making a lot of things a lot easier, but it's also making new things possible. So really understanding the fastai software is something which is going to take you a long way. And the best way to really understand the fastai software well is by using the [fastai documentation](http://docs.fast.ai/).

### Keras [[49:25](https://youtu.be/BWWm4AzsdLk?t=2965)]

![](../../../../images/fastai_p1_v3/lesson_1/105.png)

So how does it compare? There's only one major other piece of software like fastai that tries to make deep learning easy to use and that's Keras. Keras is a really terrific piece of software, we actually used it for the previous courses until we switch to fastai. It runs on top of TensorFlow. It was the gold standard for making deep learning easy to use before. But life is much easier with fastai. So if you look at the last year's course exercise which is getting dogs vs. cats, fastai lets you get much more accurate (less than half the error on a validation set), training time is less than half the time, lines of code is about 1/6. The lines of code are more important than you might realize because those 31 lines of Keras code involved you making a lot of decisions, setting lots of parameters, doing lots of configuration. So that's all stuff where you have to know how to set those things to get best practice results. Or else, those 5 lines of code, any time we know what to do for you, we do it for you. Anytime we can pick a good default, we pick it for you. So hopefully you will find this a really useful library, not just for learning deep learning but for taking it a very long way.

[[50:53](https://youtu.be/BWWm4AzsdLk?t=3053)]

![](../../../../images/fastai_p1_v3/lesson_1/106.png)

How far can you take it? All of the research that we do at fastai uses the library and an example of the research we did which was recently featured in [Wired](https://www.wired.com/story/ai-can-recognize-images-but-understand-headline/) describes a new breakthrough in a natural language processing which people are calling the ImageNet moment which is basically we broke a new state-of-the-art result in text classification which OpenAI then built on top of our paper with more computing, more data to do different tasks to take it even further. This is an example of something we've done in the last 6 months in conjunction with my colleague Sebastian Ruder - an example of something that's being built in the fastai library and you are going to learn how to use this brand new model in three lessons time. You're actually going to get this exact result from this exact paper yourself.

[[51:50](https://youtu.be/BWWm4AzsdLk?t=3110)]

![](../../../../images/fastai_p1_v3/lesson_1/107.png)

Another example, one of our alumni, [Hamel Husain built a new system for natural language semantic code search](https://githubengineering.com/towards-natural-language-semantic-code-search/), you can find it on Github where you can actually type in English sentences and find snippets of code that do the thing you asked for. Again, it's being built with the fastai library using the techniques you'll learn in the next seven weeks.

[[52:27](https://youtu.be/BWWm4AzsdLk?t=3147)]

The best place to learn about these things and get involved in these things is on the forums where as well as categories for each part of the course and there is also a general category for deep learning where people talk about research papers applications.

Even though today, we are focusing on a small number of lines of code to a particular thing which is image classification and we are not learning much math or theory, over these seven weeks and then part two, we are going to go deeper and deeper.

### Where can that take you? [[53:05](https://youtu.be/BWWm4AzsdLk?t=3185)]

![](../../../../images/fastai_p1_v3/lesson_1/108.png)

This is Sarah Hooker. She did our first course a couple of years ago. She started learning to code two years before she took our course. She started a nonprofit called Delta Analytics, they helped build this amazing system where they attached old mobile phones to trees in Kanyan rain forests and used it to listen for chainsaw noises, and then they used deep learning to figure out when there was a chainsaw being used and then they had a system setup to alert rangers to go out and stop illegal deforestation in the rainforests. That was something she was doing while she was in the course as part of her class projects.

![](../../../../images/fastai_p1_v3/lesson_1/109.png)

She is now a Google Brain researcher, publishing some papers, and now she is going to Africa to set up a Google Brain's first deep learning research center in Africa. She worked her arse off. She really really invested in this course. Not just doing all of the assignments but also going out and reading Ian Goodfellow's book, and doing lots of other things. It really shows where somebody who has no computer science or math background at all can be now one of the world's top deep learning researchers and doing very valuable work.

[[54:49](https://youtu.be/BWWm4AzsdLk?t=3289)]

![](../../../../images/fastai_p1_v3/lesson_1/110.png)

Another example from our most recent course, Christine Payne. She is now at OpenAI and you can find [her post](http://christinemcleavey.com/clara-a-neural-net-music-generator/) and actually listen to her music samples of something she built to automatically create chamber music compositions.

![](../../../../images/fastai_p1_v3/lesson_1/111.png)

She is a classical pianist. Now I will say she is not your average classical pianist. She's a classical pianist who also has a master's in medical research in Stanford, and studied neuroscience, and was a high-performance computing expert at DE Shaw, Co-Valedictorian at Princeton. Anyway. Very annoying person, good at everything she does. But I think it's really cool to see how a domain expert of playing piano can go through the fastai course and come out the other end as OpenAI fellow.

Interestingly, one of our other alumni (Sanyam Bhutani) of the course recently interviewed her for a [blog post series he is doing on top AI researchers](https://hackernoon.com/interview-with-openai-fellow-christine-mcleavey-payne-aaef948ad571) and she said one of the most important pieces of advice she got was from me and she said the advice was:

> #### Pick one project. Do it really well. Make it fantastic. [56:20](https://youtu.be/BWWm4AzsdLk?t=3380)

We're going to be talking a lot about you doing projects and making them fantastic during this course.

[[56:36](https://youtu.be/BWWm4AzsdLk?t=3396)]
Having said that, I don't really want you to go to AI or Google Brain. What I really want you to do is to go back to your workplace or your passion project and apply these skills there.

![](../../../../images/fastai_p1_v3/lesson_1/112.png)

MIT released a deep learning course and they highlighted in their announcement this medical imaging example. One of our students Alex who is a radiologist said you guys just showed a model overfitting. I can tell because I am a radiologist and this is not what this would look like on a chest film. This is what it should look like and as a deep learning practitioner, this is how I know this is what happened in your model. So Alex is combining his knowledge of radiology and his knowledge of deep learning to assess MIT's model from just two images very accurately. So this is actually what I want most of you to be doing is to take your domain expertise and combine it with the deep learning practical aspects you'll learn in this course and bring them together like Alex is doing here. So a lot of radiologists have actually gone through this course now and have built journal clubs and American Council of Radiology practice groups. There's a data science institute at the ACR now and Alex is one of the people who is providing a lot of leadership in this area. And I would love you to do the same kind of thing that Alex is doing which is to really bring deep learning leadership into your industry and to your social impact project, whatever it is that you are trying to do.

[[58:22](https://youtu.be/BWWm4AzsdLk?t=3502)]

![](../../../../images/fastai_p1_v3/lesson_1/113.png)

Another great example. This is Melissa Fabros who is a English literature PhD who studied gendered language in English literature or something and actually Rachel at the previous job taught her to code. Then she came to the fastai course. She helped Kiva, a micro lending a social impact organization, to build a system that can recognize faces. Why is that necessary? We're going to be talking a lot about this but because most AI researchers are white men, most computer vision software can only recognize white male faces effectively. In fast, I think it was IBM system was like 99.8% accurate on common white face men versus 65% accurate on dark skinned women. So it's like 30 or 40 times worse for black women versus white men. This is really important because for Kiva, black women perhaps are the most common user base for their micro lending platform. So Melissa after taking our course, again working her arse off, and being super intense in her study and her work won this $1,000,000 AI challenge for her work for Kiva.

[[59:53](https://youtu.be/BWWm4AzsdLk?t=3593)]

![](../../../../images/fastai_p1_v3/lesson_1/114.png)

Karthik did our course and realized that the thing he wanted to do wasn't at his company. It was something else which is to help blind people to understand the world around them. So he started a new startup called envision. You can download the app and point your phone to things and it will tell you what it sees. I actually talked to a blind lady about these kinds of apps the other day and she confirmed to me this is a super useful thing for visually disabled users.

[[1:00:24](https://youtu.be/BWWm4AzsdLk?t=3624)]

![](../../../../images/fastai_p1_v3/lesson_1/115.png)

The level that you can get to, with the content that you're going to get over these seven weeks and with this software can get you right to the cutting edge in areas you might find surprising. I helped [a team of some of our students and some collaborators on actually breaking the world record for how quickly you can train ImageNet](https://www.technologyreview.com/s/611858/small-team-of-ai-coders-beats-googles-code/). We used standard AWS cloud infrastructure, cost of $40 of compute to train this model using fastai library, the technique you learn in this course. So it can really take you a long way. So don't be put off by this what might seem pretty simple at first. We are going deeper and deeper.

[[1:01:17](https://youtu.be/BWWm4AzsdLk?t=3677)]

![](../../../../images/fastai_p1_v3/lesson_1/116.png)

You can also use it for other kinds of passion project. Helena Sarin - you should definitely check out her Twitter account [@glagolista](https://twitter.com/glagolista). This art is basically a new style of art that she's developed which combines her painting and drawing with generative adversarial models to create these extraordinary results. I think this is super cool. She is not a professional artists, she is a professional software developer but she keeps on producing these beautiful results. When she started, her art had not really been shown or discussed anywhere, now there's recently been some quite high profile article describing how she is creating a new form of art.

![](../../../../images/fastai_p1_v3/lesson_1/117.png)

Equally important, Brad Kenstler who figured out how to make a picture of Kanye out of pictures of Patrick Stewart's head. Also something you will learn to do if you wish to. This particular type of what's called "style transfer" - it's a really interesting tweak that allowed him to do something that hadn't quite been done before. This particular picture helped him to get a job as a deep learning specialist at AWS.

[[1:02:41](https://youtu.be/BWWm4AzsdLk?t=3761)]

Another alumni actually worked at Splunk as a software engineer and he designed an algorithm which basically turned Splunk to be fantastically good at identifying fraud and we'll talk more about it shortly.

![](../../../../images/fastai_p1_v3/lesson_1/118.png)

If you've seen Silicon Valley, the HBO series, the hotdog Not Hotdog app - that's actually a real app you can download and it was built by Tim Anglade as a fastai student project. So there's a lot of cool stuff that you can do. It was Emmy nominated. We only have one Emmy nominated fastai alumni at this stage, so please help change that.

![](../../../../images/fastai_p1_v3/lesson_1/119.png)
[[1:03:30](https://youtu.be/BWWm4AzsdLk?t=3810)]

The other thing, the forum thread can turn into these really cool things. So Francisco was a really boring McKinsey consultant like me. So Francisco and I both have this shameful past that we were McKinsey consultants, but we left and we're okay now. He started this [thread](https://forums.fast.ai/t/language-model-zoo-gorilla/14623) saying like this stuff we've just been learning about building NLP in different languages, let's try and do lots of different languages, and he started this thing called the language model zoo and out of that, there's now been an academic competition was won in Polish that led to an academic paper, Thai state of the art, German state of the art, basically as students have been coming up with new state of the art results across lots of different languages and this all is entirely done by students working together through the forum.

So please get on the forum. But don't be intimidated because everybody you see on the forum, the vast majority of posting post all the darn time. They've been doing this a lot and they do it a lot of the time. So at first, it can feel intimidating because it can feel like you're the only new person there. But you're not. You're all new people, so when you just get out there and say like "okay all you people getting these state of the art results in German language modeling, I can't start my server, I try to click the notebook and I get an error, what do I do?" People will help you. Just make sure you provide all the information ([how to ask for help](https://forums.fast.ai/t/how-to-ask-for-help/10421)).

Or if you've got something to add! If people are talking about crop yield analysis and you're a farmer and you think oh I've got something to add, please mention it even if you are not sure it's exactly relevant. It's fine. Just get involved. Because remember, everybody else in the forum started out also intimidated. We all start out not knowing things. So just get out there and try it!

[[1:05:59](https://youtu.be/BWWm4AzsdLk?t=3959)]
**Question**:question:: Why are we using ResNet as opposed to Inception?

There are lots of architectures to choose from and it would be fair to say there isn't one best one but if you look at things like the [Stanford DAWNBench benchmark of ImageNet classification](https://dawn.cs.stanford.edu/benchmark/#imagenet), you'll see in first place, second place, third place, and fourth place all use ResNet. ResNet is good enough, so it's fine. :laughing::laughing::laughing:

![](../../../../images/fastai_p1_v3/lesson_1/120.png)

The main reason you might want a different architecture is if you want to do edge computing, so if you want to create a model that's going to sit on somebody's mobile phone. Having said that, even there, most of the time, I reckon the best way to get a model onto somebody's mobile phone is to run it on your server and then have your mobile phone app talk to it. It really makes life a lot easier and you get a lot more flexibility. But if you really do need to run something on a low powered device, then there are special architectures for that. So the particular question was about Inception. That's a particular another architecture which tends to be pretty memory intensive but it's okay. It's not terribly resilient. One of the things we try to show you is stuff which just tends to always work even if you don't quite tune everything perfectly. So ResNet tends to work pretty well across a wide range of different kind of details around choices that you might make. So I think it's pretty good.

[[1:07:58](https://youtu.be/BWWm4AzsdLk?t=4078)]

We've got this trained model and what's actually happened as we'll learn is it's basically creating a set of weights. If you've ever done anything like a linear regression or logistic regression, you'll be familiar with coefficients. We basically found some coefficients and parameters that work pretty well and it took us a minute and 56 seconds. So if we want to start doing some more playing around and come back later, we probably should save those weights. You can just go `learn.save` and give it a name. It's going to put it in a model subdirectory in the same place the data came from, so if you save different models or different DataBunches from different datasets, they'll all be kept separate. So don't worry about it.

```python
learn.save('stage-1')
```

## Results [[1:08:54](https://youtu.be/BWWm4AzsdLk?t=4134)]

To see what comes out, we could use this class for class interpretation. We are going to use this factory method from learner, so we pass in a learn object. Remember a learn object knows two things:

1. What's your data
2. What is your model. Now it's not just an architecture, it's actually a trained model

That's all the information we need to interpret that model.

```python
interp = ClassificationInterpretation.from_learner(learn)
```

One of the things, perhaps the most useful things to do is called `plot_top_losses`. We are going to be learning a lot about this idea of loss functions shortly but in short, a loss function is something that tells you how good was your prediction. Specifically that means if you predicted one class of cat with great confidence, but actually you were wrong, then that's going to have a high loss because you were very confident about the wrong answer. So that's what it basically means to have high loss. By plotting the top losses, we are going to find out what were the things that we were the most wrong on, or the most confident about what we got wrong.

```python
interp.plot_top_losses(9, figsize=(15,11))

```
![](../../../../images/fastai_p1_v3/lesson_1/9.png)

It prints out four things. What do they mean? Perhaps we should look at the document.

We have already seen `help`, and `help` just prints out a quick little summary. But if you want to really see how to do something use `doc`.

![](../../../../images/fastai_p1_v3/lesson_1/121.png)

`doc` tells you the same information as `help` but it has this very important thing which is `Show in docs`. When you click on it, it pops up the documentation for that method or class or function or whatever:

![](../../../../images/fastai_p1_v3/lesson_1/122.png)

It starts out by showing us the same information about what are the parameters it takes a long with the docstring. But then tells you more information:

> The title of each image shows: prediction, actual, loss, probability of actual class.

The documentation always has working code. This is your friend when you're trying to figure out how to use these things. The other thing I'll mention is if you're somewhat experienced Python programmer, you'll find the source code of fastai really easy to read. We are trying to write everything in just a small number (much less than half a screen) of code. If you click on `[source]` you can jump straight to the source code.

![](../../../../images/fastai_p1_v3/lesson_1/123.png)

Here is `plot_top_loss`, and this is also a great way to find out how to use the fastai library. Because nearly every line of code here, is calling stuff in the fastai library. So don't be afraid to look at the source code.

[[1:12:48](https://youtu.be/BWWm4AzsdLk?t=4368)]

So that's how we can look at top losses and these are perhaps the most important image classification interpretation tools that we have because it lets us see what we are getting wrong.

:loudspeaker: _fastai had a bug when this code was run - your numbers will look different to this!_

In this case, if you are a dog and cat expert, you'll realize that the things that's getting wrong are breeds that are actually very difficult to tell apart and you'd be able to look at these and say "oh I can see why they've got this one wrong". So this is a really useful tool.

### Confusion matrix [[1:13:21](https://youtu.be/BWWm4AzsdLk?t=4401)]

Another useful tool, kind of, is to use something called a confusion matrix which basically shows you for every actual type of dog or cat, how many times was it predicted to be that dog or cat. But unfortunately, in this case, because it's so accurate, this diagonal basically says how it's pretty much right all the time.
![](../../../../images/fastai_p1_v3/lesson_1/10.png)

And you can see there is slightly darker ones like a five here, it's really hard to read exactly what their combination is. So what I suggest you use is instead of, if you've got lots of classes, don't use confusion matrix, but this is my favorite named function in fastai and I'm very proud of this - you can call "most confused".

### Most confused [[1:13:52](https://youtu.be/BWWm4AzsdLk?t=4432)]

```python
interp.most_confused(min_val=2)

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
[('american_pit_bull_terrier', 'staffordshire_bull_terrier', 6),
 ('Birman', 'Ragdoll', 5),
 ('english_setter', 'english_cocker_spaniel', 4),
 ('staffordshire_bull_terrier', 'american_pit_bull_terrier', 4),
 ('boxer', 'american_bulldog', 4),
 ('Ragdoll', 'Birman', 3),
 ('miniature_pinscher', 'chihuahua', 3),
 ('Siamese', 'Birman', 3)]
```

`most_confused` will simply grab out of the confusion matrix the particular combinations of predicted and actual that got wrong the most often. So this case, `('american_pit_bull_terrier', 'staffordshire_bull_terrier', 6)`:
- Actual `'american_pit_bull_terrier'`
- Prediction `'staffordshire_bull_terrier'`
- This particular combination happened 6 times.

So this is a very useful thing because you can look and say "with my domain expertise, does it make sense" that would be something that was confused about?

### Unfreezing, fine-tuning, and learning rates [[1:14:38](https://youtu.be/BWWm4AzsdLk?t=4478)]

Let's make our model better. How do we make it better? By using fine-tuning. So far we fitted 4 epochs and it ran pretty quickly. The reason it ran pretty quickly is that there was a little trick we used. These convolutional networks, they have many layers. We'll learn a lot about exactly what layers are, but for now, just know it goes through a lot of computations. What we did was we added a few extra layers to the end and we only trained those. We basically left most of the model exactly as it was, so that's really fast. If we are trying to build a model at something that's similar to the original pre-trained model (in this case, similar to the ImageNet data), that works pretty well.

But what we really want to do is to go back and train the whole model. This is why we pretty much always use this two stage process. By default, when we call `fit` or `fit_one_cycle` on a ConvLearner, it'll just fine-tune these few extra layers added to the end and it will run very fast. It will basically never overfit but to really get it good, you have to call `unfreeze`. `unfreeze` is the thing that says please train the whole model. Then I can call `fit_one_cycle` again.

```python
learn.unfreeze()
learn.fit_one_cycle(1)

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
Total time: 00:20
epoch  train_loss  valid_loss  error_rate
1      1.045145    0.505527    0.159681    (00:20)
```

Uh-oh. The error got much worse. Why? In order to understand why, we are actually going to have to learn more about exactly what's going on behind the scenes. So let's start out by trying to get an intuitive understanding of what's going on behind the scenes. We are going to do it by looking at pictures.

[[1:16:28](https://youtu.be/BWWm4AzsdLk?t=4588)]
![](../../../../images/fastai_p1_v3/lesson_1/100.png)

These pictures come from [a fantastic paper](https://cs.nyu.edu/~fergus/papers/zeilerECCV2014.pdf) by Matt Zeiler who nowadays is a CEO of Clarify which is a very successful computer vision startup and his supervisor for his PhD Rob Fergus. They wrote a paper showing how you can visualize the layers of a convolutional neural network. A convolutional neural network, which we will learn mathematically about what the layers are shortly, but the basic idea is that your red, green, and blue pixel values that are numbers from nought to 255 go into the simple computation (i.e. the first layer) and something comes out of that, and then the result of that goes into a second layer, and the result of that goes into the third layer and so forth. There can be up to a thousand layers of neural network. ResNet34 has 34 layers, and ResNet50 has 50 layers, but let's look at layer one. There's this very simple computation which is a convolution if you know what they are. What comes out of this first layer? Well, we can actually visualize these specific coefficients, the specific parameters by drawing them as a picture. There's actually a few dozen of them in the first layer, so we don't draw all of them. Let's just look at 9 at random.

[[1:17:45](https://youtu.be/BWWm4AzsdLk?t=4665)]

![](../../../../images/fastai_p1_v3/lesson_1/124.png)

Here are nine examples of the actual coefficients from the first layer. So these operate on groups of pixels that are next to each other. So this first one basically finds groups of pixels that have a little diagonal line, the second one finds diagonal line in the other direction, the third one finds gradients that go from yellow to blue, and so forth. They are very simple little filters. That's layer one of ImageNet pre-trained convolutional neural net.
<br>`다음은 첫 번째 층의 실제 계수의 9가지 예제 입니다. 그래서 이것들은 서로 옆에 있는 픽셀 그룹으로 작동한다. 첫번째는 기본적으로 약간 대각선을 가진 픽셀 그룹을 찾고, 두번째는 다른 방향에서 대각선을 찾고, 세번째는 노란색에서 파란색으로 가는 gradient를 찾는 겁니다. 그것들은 아주 간단한 작은 필터들이다. 이건 ImageNet의 사전 훈련된 convolutional 신경망 중 하나이다.`

![](../../../../images/fastai_p1_v3/lesson_1/125.png)

Layer 2 takes the results of those filters and does a second layer of computation. The bottom right are nine examples of a way of visualizing one of the second layer features. AS you can see, it basically learned to create something that looks for top left corners. There are ones that learned to find right-hand curves, and little circles, etc. In layer one, we have things that can find just one line, and in layer 2, we can find things that have two lines joined up or one line repeated. If you then look over to the right, these nine show you nine examples of actual bits of the actual photos that activated this filter a lot. So in other words, the filter on the bottom right was good at finding these window corners etc.
<br>`Layer 2는 이러한 필터의 결과를 취하여 두 번째 layer를 계산한다. 오른쪽 아래는 두 번째 layer 특징 중 하나를 시각화하는 방법의 9가지 예들이다. 보시다시피, 왼쪽 위 모서리를 찾는 것을 기본적으로 배웠다. 오른쪽 곡선, 작은 원 등을 찾는 법을 배운 것이 있다. layer 1 에는 한 줄만 찾을 수 있는 것들이 있고, layer 2 에는 두 줄이 연결되어 있거나 한 줄이 반복되어 있는 것들을 발견할 수 있다. 오른쪽을 보시면, 이 9개의 사진은 실제 사진의 9개의 예를 볼 수 있는데, 이 필터를 많이 활성화시킨 겁니다. 즉, 오른쪽 하단의 필터는 이러한 창구석 등을 잘 찾아냈던 것이다.`

So this is the kind of stuff you've got to get a really good intuitive understanding for. The start of my neural net is going to find very simple gradients and lines, the second layer can find very simple shapes, the third layer can find  combination of those.
<br>`이것은 여러분이 정말 좋은 직관적인 이해를 얻어야 하는 것 입니다. 나의 신경망의 시작은 매우 단순한 구배와 선을 찾을 것이고, 두 번째 layer은 매우 단순한 모양을 찾을 수 있을 것이고, 세 번째 layer은 그것들의 조합을 찾을 수 있을 것이다.`

![](../../../../images/fastai_p1_v3/lesson_1/126.png)

Now we can find repeating pattern of two dimensional objects or we can find things that joins together, or bits of text (although sometimes windows) - so it seems to find repeated horizontal patterns. There are also ones that seem to find edges of fluffy or flowery things or geometric patterns. So layer 3 was able to take all the stuff from layer 2 and combine them together.
<br>`이제 우리는 2차원 물체의 반복적인 패턴을 찾을 수 있고, 함께 결합되는 사물이나 텍스트의 일부(때로는 창도 있지만)를 찾을 수 있어 반복적인 수평 패턴을 찾을 수 있는 것처럼 보인다. 솜털이나 꽃무늬의 가장자리나 기하학적 무늬를 찾아내는 듯한 것도 있다. 그래서 세번째 레이어은 두번째 레이어으로부터 모든 물질들을 가져다가 결합시킬 수 있었다.`

![](../../../../images/fastai_p1_v3/lesson_1/127.png)

Layer 4 can take all the stuff from layer 3 and combine them together. By layer 4, we got something that can find dog faces or bird legs.
<br>`Layer 4는 layer 3의 모든 물질을 취해서 결합시킬 수 있다. layer 4에는 개 얼굴이나 새 다리를 찾을 수 있는 무언가가 있다.`

By layer 5, we've got something that can find the eyeballs of bird and lizards, or faces of particular breeds of dogs and so forth. So you can see how by the time you get to layer 34, you can find specific dog breeds and cat breeds. This is kind of how it works.
<br>`layer 5에는 새와 도마뱀의 눈알이나 특정 종의 개들의 얼굴을 찾을 수 있는 무언가가 있다. layer 34에 이르면 특정 개 품종과 고양이 품종을 찾을 수 있는 방법을 알 수 있다. 이런 식으로 되는 겁니다.`

So when we first trained (i.e. fine-tuned) the pre-trained model, we kept all of these layers that you've seen so far and we just trained a few more layers on top of all of those sophisticated features that are already being created. So now we are going back and saying "let's change all of these". We will start with where they are, but let's see if we can make them better.
<br>`그래서 우리가 처음 pre-trained 모델을 학습시켰을 때(즉, fine-tuned) 지금까지 보셨던 모든 layer을 유지했고, 이미 만들어지고 있는 모든 정교한 특징들 위에 몇 개의 layer를 더 훈련시켰을 뿐이었습니다. 그래서 이제 우리는 돌아가서 "이 모든 것을 바꾸자"고 말할 것이다. 우리는 그들이 어디에 있는지부터 시작할 것이다. 하지만 우리가 그들을 더 낫게 만들 수 있는지 보자.`

Now, it seems very unlikely that we can make layer 1 features better. It's very unlikely that the definition of a diagonal line is going to be different when we look at dog and cat breeds versus the ImageNet data that this was originally trained on. So we don't really want to change the layer 1 very much if at all. Or else, the last layers, like types of dog face seems very likely that we do want to change that. So **you want this intuition, this understanding that the different layers of a neural network represents different level of semantic complexity**.
<br>`이제, 우리가 layer 1 특징을 더 잘 만들 수 있을 것 같지는 않다. 우리가 개와 고양이 품종을 볼 때 대각선 선의 정의는 원래 훈련되었던 ImageNet 데이터와 다를 것 같지 않다. 그래서 우리는 정말로 layer 1을 아주 많이 바꾸고 싶지 않다. 아니면, 마지막 layer는, 개 얼굴 형태와 같은, 우리가 그것을 바꾸고 싶어할 가능성이 매우 높아 보인다. 그래서 여러분은 이 직관을 원하시겠죠, 신경망의 다른 layer가 다른 의미적 복잡성의 수준을 나타낸다는 것을 이해하시겠죠`

[[1:22:06](https://youtu.be/BWWm4AzsdLk?t=4926)]

This is why our attempt to fine-tune this model didn't work because by default, it trains all the layers at the same speed which is to say it will update those things representing diagonal lines and gradients just as much as it tries to update the things that represent the exact specifics of what an eyeball looks like, so we have to change that.
<br>`이것이 우리가 이 모델을 fine-tune하려는 시도가 효과가 없었던 이유인데, 왜냐하면 그것은 기본적으로 모든 층을 동일한 속도로 훈련하기 때문인데, 그것은 눈알이 어떻게 보이는지 정확하게 나타내는 것들을 업데이트하려는 것만큼 대각선이나 구배를 나타내는 것들을 업데이트할 것이기 때문이다. 그래서 우리는 그것을 바꿔야 한다.`

To change it, we first of all need to go back to where we were before. We just broke this model, much worse than it started out. So if we just go:
<br>`그것을 바꾸기 위해서는 무엇보다도 우리가 전에 있던 곳으로 돌아가야 한다. 우리는 이 모델을 막 부숴버렸어. 시작했던 것보다 훨씬 더 안 좋아. 그래서 만약 우리가 그냥 간다면:`

```python
learn.load('stage-1')
```

This brings back the model that we saved earlier. So let's load that back up and now our models back to where it was before we killed it.
<br>`이것은 우리가 이전에 저장했던 model로 되돌려 준다. 그럼 그걸 다시 올려서 우리가 죽이기 전에 원래 있던 곳으로 model을 되돌려 놓자.`

### Learning rate finder [[1:22:58](https://youtu.be/BWWm4AzsdLk?t=4978)]

Let's run learning rate finder. We are learning about what that is next week, but for now, just know this is the thing that figures out what is the fastest I can train this neural network at without making it zip off the rails and get blown apart.
<br>`learning rate 검색기를 실행해 봅시다. 우리는 그것이 다음 주에 무엇인지 알아 볼건데, 지금으로서는, 이것이 내가 이 신경망을 레일에서 지퍼를 내리고 산산조각이 나지 않도록 훈련할 수 있는 가장 빠른 값을 알아내는 것이다.`

```python
learn.lr_find()
learn.recorder.plot()
```

![](../../../../images/fastai_p1_v3/lesson_1/11.png)

This will plot the result of our LR finder and what this basically shows you is this key parameter called a learning rate. The **learning rate basically says how quickly am I updating the parameters in my model**. The x-axis one here shows me what happens as I increase the learning rate. The y axis show what the loss is. So you can see, once the learning rate gets passed 10^-4, my loss gets worse. It actually so happens, in fact I can check this if I press <kbd>shift</kbd>+<kbd>tab</kbd> here, my learning defaults to 0.003. So you can see why our loss got worse. Because we are trying to fine-tune things now, we can't use such a high learning rate. So based on the learning rate finder, I tried to pick something well before it started getting worse. So I decided to pick `1e-6`. But there's no point training all the layers at that rate, because we know that the later layers worked just fine before when we were training much more quickly. So what we can actually do is we can pass a range of learning rates to `learn.fit_one_cycle`. And we do it like this:
<br>`이것은 우리의 LR 검색기의 결과를 나타낼 것이고 기본적으로 당신에게 보여지는 것은 learning rate라고 불리는 이 핵심 파라미터다. **learning rate는 기본적으로 내 모델의 매개변수를 얼마나 신속히 업데이트하고 있는지 알려준다**. 여기 x축은 learning rate를 증가시킬 때 어떤 일이 일어나는지 보여 준다. Y축은 loss가 무엇인지 보여준다. 그러니까, 일단 학습률이 10^-4를 넘으면, 손실은 더 심해진다. 실제로 그렇게 되는데, 사실 여기서 <kbd>shift </kbd>+<kbd>tab </kbd>를 누르면 나의 학습은 0.003으로 기본이 된다. 그래서 우리의 손실이 왜 더 심해졌는지를 알 수 있다. 우리는 지금 사물을 미세 조정하려고 하기 때문에, 그렇게 높은 learning rate를 사용할 수 없다. 그래서 learning rate 검색기를 바탕으로, 나는 그것이 더 악화되기 전에 무언가를 고르려고 노력했다. 그래서 '1e-6'을 뽑기로 했다. 하지만 그런 속도로 모든 layer들을 훈련시키는 것은 무의미하다. 왜냐하면 우리가 훨씬 더 빨리 훈련을 할 때 그 이전 레이어들이 잘 작동한다는 것을 알기 때문이다. 그래서 우리가 실제로 할 수 있는 것은 다양한 learning rate를 'learn.fit_one_cycle' 에 전달할 수 있는 것이다. 이런 식으로 말이다.`

```python
learn.unfreeze()
learn.fit_one_cycle(2, max_lr=slice(1e-6,1e-4))

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
Total time: 00:41
epoch  train_loss  valid_loss  error_rate
1      0.226494    0.173675    0.057219    (00:20)
2      0.197376    0.170252    0.053227    (00:20)
```

You use this keyword in Python called `slice` and that can take a start value and a stop value and basically what this says is train the very first layers at a learning rate of 1e-6, and the very last layers at a rate of 1e-4, and distribute all the other layers across that (i.e. between those two values equally).
<br>`당신은 'slice'라고 불리는 python에서 이 키워드를 사용하며, 그것은 시작 값과 정지 값을 취할 수 있으며, 기본적으로 이것이 말하는 것은 1e-6의 learning rate로 첫 번째 layer를 훈련시키고, 1e-4의 속도로 마지막 layer을 훈련시키고, 다른 모든 layer을 그 전체로 분배하는 것이다(즉, 두 개의 값 사이에서 똑같이).`

### How to pick learning rates after unfreezing [[1:25:23](https://youtu.be/BWWm4AzsdLk?t=5123)]

A **good rule of thumb is after you unfreeze** (i.e. train the whole thing), pass a max learning rate parameter, pass it a slice, make the second part of that slice about 10 times smaller than your first stage. Our first stage defaulted to about 1e-3 so it's about 1e-4. And the first part of the slice should be a value from your learning rate finder which is well before things started getting worse. So you can see things are starting to get worse maybe about here:
<br>`**즉, 모든 것을 훈련시키고, 최대 학습 속도 파라미터를 통과시켜 슬라이스의 두 번째 부분을 첫 번째 단계보다 약 10배 작게 만드는 것이 엄지손가락의 좋은 규칙이다. 우리의 첫 번째 stage는 약 1e-3으로 디폴트되어 약 1e-4이다. 그리고 이 slice의 첫 부분은 상황이 악화되기 훨씬 전에 당신의 learning rate 검색기에서 얻은 가치여야 한다. 상황이 더 나빠지기 시작했다는 걸 알 수 있을 겁니다`

![](../../../../images/fastai_p1_v3/lesson_1/128.png)

So I picked something that's at least 10 times smaller than that.
<br>`그래서 그것보다 최소 10배는 작은 것을 골랐다.`

If I do that, then the error rate gets a bit better. So I would perhaps say for most people most of the time, these two stages are enough to get pretty much a world-class model. You won't win a Kaggle competition, particularly because now a lot of fastai alumni are competing on Kaggle and this is the first thing that they do. But in practice, you'll get something that's about as good in practice as the vast majority of practitioners can do.
<br>`그렇게 하면 오류율이 좀 좋아진다. 그래서 아마 대부분의 사람들에게 이 두 단계는 세계 수준의 모델을 얻기에 충분하다고 말할 수 있을 겁니다. 당신은 Kaggle 대회에서 우승하지 못할 것이다. 특히 지금은 많은 fastai 동문들이 Kaggle에서 경쟁하고 있고 이것이 그들이 하는 첫 번째 일이기 때문이다. 그러나 실제로 당신은 대다수의 실무자들이 할 수 있는 것만큼 좋은 것을 얻게 될 것이다.`

## ResNet50 [[1:26:55](https://youtu.be/BWWm4AzsdLk?t=5215)]

We can improve it by using more layers and we will do this next week but by basically doing a ResNet50 instead of ResNet34. And you can try running this during the week if you want to. You'll see it's exactly the same as before, but I'm using ResNet50.
<br>`우리는 더 많은 layer를 사용함으로써 그것을 개선할 수 있고 우리는 다음 주에 이것을 할 것이다. 그러나 기본적으로 ResNet34 대신 ResNet50을 한다. 그리고 네가 원한다면 일주일 동안 이것을 실행해 볼 수 있다. 이전과 똑같아 보이겠지만, 나는 ResNet50을 사용하고 있다.`

```python
data = ImageDataBunch.from_name_re(path_img, fnames, pat, ds_tfms=get_transforms(), size=320, bs=bs//2)
data.normalize(imagenet_stats)
```

```python
learn = ConvLearner(data, models.resnet50, metrics=error_rate)
```

What you'll find is it's very likely if you try to do this, you will get an error and the error will be your GPU has ran out of memory. The reason for that is that ResNet50 is bigger than ResNet34, and therefore, it has more parameters and use more of your graphics card memory, just totally separate to your normal computer RAM, this is GPU RAM. If you're using the default Salamander, AWS, and so forth, then you'll be having a 16G of GPU memory. The card I use most of the time has 11G GPU memory, the cheaper ones have 8G. That's kind of the main range you tend to get. If yours have less than 8G of GPU memory, it's going to be frustrating for you.
<br>`여러분이 발견하게 될 것은 만약 여러분이 이것을 하려고 한다면, 여러분은 오류를 얻게 될 것이고, 오류는 여러분의 GPU의 메모리가 부족하게 될 것이라는 것이다. 그 이유는 ResNet50이 ResNet34보다 더 크기 때문이다. 따라서, 그것은 더 많은 파라미터를 가지고 있고 그래픽 카드 메모리를 더 많이 사용하기 때문이다. 단지 당신의 일반적인 컴퓨터 RAM과 완전히 분리되어 있다. 이것은 GPU RAM이다. 기본 Salamander, AWS 등을 사용하고 있다면 16G의 GPU 메모리를 갖게 될 겁니다. 내가 대부분의 시간을 사용하는 카드는 11G GPU 메모리를 가지고 있고, 더 싼 카드는 8G를 가지고 있다. 그게 네가 얻는 주요 범위야. 만약 당신의 GPU 메모리가 8G 미만이면, 그것은 당신에게 좌절감을 줄 것이다.`

It's very likely that if you try to run this, you'll get an out of memory error and that's because it's just trying to do too much - too many parameter updates for the amount of RAM you have. That's easily fixed. `ImageDataBunch` constructor has a parameter at the end `bs` - a batch size. This basically says how many images do you train at one time. If you run out of memory, just make it smaller.
<br>`이것을 실행하려고 하면 메모리 부족 오류가 발생할 가능성이 매우 높고, 그것은 당신이 가지고 있는 RAM의 양에 비해 너무 많은 매개 변수 업데이트를 너무 많이 하려고 하기 때문이다. 그것은 쉽게 고쳐진다. ImageDataBunch의 생성자는 배치 크기인 'bs'라는 파라미터를 가지고 있다. 이것은 기본적으로 한번에 얼마나 많은 이미지들을 훈련시키는지 말해준다. 메모리가 부족하면 이 값을 줄인다.`

It's fine to use a smaller batch size. It might take a little bit longer. That's all. So that's just one number you'll need to try during the week.
<br>`더 작은 batch size로 사용해도 좋다. 조금 더 걸릴 수도 있다. 그게 다야. 그러니까 한 주 동안 시도해 봐야 할 숫자야.`

```python
learn.fit_one_cycle(8, max_lr=slice(1e-3))

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
Total time: 07:08
epoch  train_loss  valid_loss  error_rate
1      0.926640    0.320040    0.076555    (00:52)
2      0.394781    0.205191    0.063568    (00:52)
3      0.307754    0.203281    0.069036    (00:53)
4      0.244182    0.160488    0.054682    (00:53)
5      0.185785    0.153520    0.049214    (00:53)
6      0.157732    0.149660    0.047163    (00:53)
7      0.107212    0.136898    0.043062    (00:53)
8      0.097324    0.136638    0.042379    (00:54)
```

Again, we fit it for a while and we get down to 4.2% error rate. So this is pretty extraordinary. I was pretty surprised because when we first did in the first course, this cats vs. dogs, we were getting somewhere around 3% error for something where you've got a 50% chance of being right and the two things look totally different. So the fact that we can get 4.2% error for such a fine grain thing, it's quite extraordinary.
<br>`다시 한 번 말씀드리지만, 우리는 그것을 잠시 맞추고 4.2%의 오류율을 얻는다. 그래서 이것은 매우 특별하다. 나는 꽤 놀랐어. 왜냐하면 우리가 처음 첫번째 코스에서 이 고양이들과 개들을 상대로 했을 때, 우리는 약 3%의 오류를 범하고 있었는데, 그것은 당신이 옳을 확률은 50%이고 두 가지는 완전히 다르게 생겼기 때문이야. 그래서 이렇게 미세한 곡물에 대해서 4.2%의 오차를 얻을 수 있다는 것은 상당히 이례적이다.`

### Interpreting the results again [[1:29:41](https://youtu.be/BWWm4AzsdLk?t=5381)]

```python
interp = ClassificationInterpretation.from_learner(learn)
interp.most_confused(min_val=2)

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
[('Ragdoll', 'Birman', 7),
 ('american_pit_bull_terrier', 'staffordshire_bull_terrier', 6),
 ('Egyptian_Mau', 'Bengal', 6),
 ('Maine_Coon', 'Bengal', 3),
 ('staffordshire_bull_terrier', 'american_pit_bull_terrier', 3)]
```

You can call the most_confused here and you can see the kinds of things that it's getting wrong. Depending on when you run it, you're going to get slightly different numbers, but you'll get roughly the same kind of things. So quite often, I find the Ragdoll and Birman are things that it gets confused. I actually have never heard of either of those things, so I actually looked them up and found a page on the cat site called "Is this a Birman or Ragdoll kitten?" and there was a long thread of cat experts arguing intensely about which it is. So I feel fine that my computer had problems. :laughing::laughing::laughing:
<br>`당신은 여기서 가장 혼란스러운 것을 부를 수 있고 당신은 그것이 잘못되고 있는 종류의 것들을 볼 수 있다. 언제 실행하느냐에 따라 조금씩 다른 숫자가 나오겠지만 대략 같은 종류의 것들이 나올 겁니다. 꽤 자주, 나는 Ragdoll과 Birman이 혼란스러운 것이라는 것을 발견한다. 나는 실제로 그런 것들에 대해 들어본 적이 없어서 실제로 그것들을 찾아봤더니 고양이 사이트에서 "이게 비르만인가 라그돌 새끼인가?"라는 페이지를 찾았는데, 고양이 전문가들이 어떤 것인지 격렬하게 논쟁을 벌이는 긴 실마리가 있었다. 그래서 나는 내 컴퓨터에 문제가 있어서 기분이 좋다.`

![](../../../../images/fastai_p1_v3/lesson_1/129.png)

I found something similar, I think it was this pitbull versus staffordshire bull terrier, apparently the main difference is the particular kennel club guidelines as to how they are assessed. But some people think that one of them might have a slightly redder nose. So this is the kind of stuff where actually even if you're not a domain expert, it helps you become one. Because I now know more about which kinds of pet breeds are hard to identify than I used to. So model interpretation works both ways.
<br>`나는 비슷한 것을 발견했는데, 나는 이 핏불 대 스태포드셔의 불테리어라고 생각한다. 분명히 주된 차이점은 그들이 어떻게 평가되는지에 대한 특별한 협회의 지침이다. 하지만 어떤 사람들은 그들 중 한 명이 약간 더 빨간 코를 가지고 있을 수도 있다고 생각한다. 이런 종류의 것들은 여러분이 도메인 전문가가 아니더라도 여러분이 하나가 되는 데 도움이 되는 겁니다. 왜냐하면 나는 이제 예전에 비해 어떤 종류의 애완동물을 식별하기 어려운지 더 많이 알고 있기 때문이다. 따라서 모델 해석은 두 가지 방식으로 모두 작용한다.`

## Homework [[1:30:58](https://youtu.be/BWWm4AzsdLk?t=5458)]

So what I want you to do this week is to run this notebook, make sure you can get through it, but then I really want you to do is to get your own image dataset and actually Francisco who is now helping to TA the course is putting together a guide that will show you how to download data from Google Images so you can create your own dataset to play with. But before I do, I want to show you how to create labels in lots of different ways because your dataset where you get it from won't necessarily be that kind of regex based approach. It could be in lots of different formats. So to show you how to do this, I'm going to use the MNIST sample. MNIST is a picture of hand drawn numbers - just because I want to show you different ways of creating these datasets.
<br>`그래서 이번 주에 여러분이 이 notebook을 실행하고, 여러분이 이 notebook을 사용할 수 있도록 확실히 해 두었으면 합니다만, 저는 여러분이 정말로 하고 싶은 것은 여러분만의 이미지 데이터셋을 얻는 것입니다, 그리고 지금 TA 과정을 돕고 있는 프란시스코는 여러분이 구글 이미지에서 데이터를 다운로드하는 방법을 보여주는 가이드를 모아서 여러분만의 데이터셋을 만들 수 있도록 하는 겁니다.하지만 그러기 전에, 라벨을 만드는 방법을 여러 가지 다양한 방법으로 보여드리고 싶다. 왜냐하면 데이터 세트가 반드시 정규식 기반 접근방식같은 것이 될 필요는 없기 때문이다. 그것은 많은 다른 형태일 수 있다. 그래서 이걸 어떻게 하는지 보여드리기 위해서 MNIST 샘플을. MNIST는 손으로 그린 숫자의 그림이다. 단지 내가 당신에게 이 데이터셋을 만드는 다른 방법을 보여주고 싶기 때문이다.`

```python
path = untar_data(URLs.MNIST_SAMPLE); path
```

```python
path.ls()

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
['train', 'valid', 'labels.csv', 'models']
```

You see there are a training set and the validation set already. So basically the people that put together this dataset have already decided what they want you to use as a validation set.

### Possibility 1: Labels are folder names

```python
(path/'train').ls()

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
['3', '7']
```

There are a folder called 3 and a folder called 7. Now this is really common way to give people labels. Basically it says everything that's a three, I put in a folder called three. Everything that's a seven, I'll put in a folder called seven. This is often called an "ImageNet style dataset" because this is how ImageNet is distributed. So if you have something in this format where the labels are just whatever the folders are called, you can say `from_folder`.

```python
tfms = get_transforms(do_flip=False)
data = ImageDataBunch.from_folder(path, ds_tfms=tfms, size=26)
```

This will create an `ImageDataBunch` for you and as you can see it created the labels:

```python
data.show_batch(rows=3, figsize=(5,5))
```

![](../../../../images/fastai_p1_v3/lesson_1/12.png)

### Possibility 2: CSV file [[1:33:17](https://youtu.be/BWWm4AzsdLk?t=5597)]

Another possibility, and for this MNIST sample, I've got both, it might come with a CSV file that would look something like this.

```python
df = pd.read_csv(path/'labels.csv')
df.head()
```

![](../../../../images/fastai_p1_v3/lesson_1/130.png)

For each file name, what's its label. In this case, labels are not three or seven, they are 0 or 1 which basically is it a 7 or not. So that's another possibility. If this is how your labels are, you can use `from_csv`:

```python
data = ImageDataBunch.from_csv(path, ds_tfms=tfms, size=28)
```

And if it is called `labels.csv`, you don't even have to pass in a file name. If it's called something else, then you can pass in the `csv_labels`

```python
data.show_batch(rows=3, figsize=(5,5))
data.classes

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
[0, 1]
```

![](../../../../images/fastai_p1_v3/lesson_1/13.png)

### Possibility 3: Using regular expression

```python
fn_paths = [path/name for name in df['name']]; fn_paths[:2]

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
[PosixPath('/home/jhoward/.fastai/data/mnist_sample/train/3/7463.png'),
 PosixPath('/home/jhoward/.fastai/data/mnist_sample/train/3/21102.png')]
```

This is the same thing, these are the folders. But I could actually grab the label by using a regular expression. We've already seen this approach:

```python
pat = r"/(\d)/\d+\.png$"
data = ImageDataBunch.from_name_re(path, fn_paths, pat=pat, ds_tfms=tfms, size=24)
data.classes

# -----------------------------------------------------------------------------
# Output
# -----------------------------------------------------------------------------
['3', '7']
```

### Possibility 4: Something more complex [[1:34:21](https://youtu.be/BWWm4AzsdLk?t=5661)]

You can create an arbitrary function that extracts a label from the file name or path. In that case, you would say `from_name_func`:

```python
data = ImageDataBunch.from_name_func(path, fn_paths, ds_tfms=tfms, size=24,
        label_func = lambda x: '3' if '/3/' in str(x) else '7')
data.classes
```

### Possibility 5: You need something even more flexible

If you need something even more flexible than that, you're going to write some code to create an array of labels. So in that case, you can just use `from_lists` and pass in the array.

```python
labels = [('3' if '/3/' in str(x) else '7') for x in fn_paths]
labels[:5]
```

```python
data = ImageDataBunch.from_lists(path, fn_paths, labels=labels, ds_tfms=tfms, size=24)
data.classes
```

So you can see there's lots of different ways of creating labels. So during the week, try this out.

Now you might be wondering how would you know to do all these things? Where am I going to find this kind of information? So I'll show you something incredibly cool. You know how to get documentation:

```python
doc(ImageDataBunch.from_name_re)
```

[[Show in docs](https://docs.fast.ai/vision.data.html#ImageDataBunch.from_name_re)]

![](../../../../images/fastai_p1_v3/lesson_1/131.png)

Here's the thing, every single line of code I just showed you, I took it this morning and I copied and pasted it from the documentation. So you can see here the exact code that I just used. So the documentation for fastai doesn't just tell you what to do, but step to step how to do it. And here is perhaps the coolest bit. If you go to [fastai/fastai_docs](https://github.com/fastai/fastai_docs) and click on [docs/src](https://github.com/fastai/fastai_docs/tree/master/docs_src).

**All of our documentation is actually just Jupyter Notebooks**. You can git clone this repo and if you run it, you can actually run every single line of the documentation yourself.

This is the kind of the ultimate example to me of experimenting. Anything that you read about in the documentation, nearly everything in the documentation has actual working examples in it with actual datasets that are already sitting in there in the repo for you. So you can actually try every single function in your browser, try seeing what goes in and try seeing what comes out.

[[1:37:27](https://youtu.be/BWWm4AzsdLk?t=5847)]
**Question**:question:: Will the library use multi GPUs in parallel by default?

The library will use multiple CPUs by default but just one GPU by default. We probably won't be looking at multi GPU until part 2. It's easy to do and you'll find it on the forum, but most people won't be needing to use that now.

**Question**:question:: Can the library use 3D data such as MRI or CAT scan?

Yes, it can. And there is actually a forum thread about that already. Although that's not as developed as 2D yet but maybe by the time the MOOC is out, it will be.

### Splunk Anti-Fraud Software [[1:38:10](https://youtu.be/BWWm4AzsdLk?t=5890)]

[Blog](https://www.splunk.com/blog/2017/04/18/deep-learning-with-splunk-and-tensorflow-for-security-catching-the-fraudster-in-neural-networks-with-behavioral-biometrics.html)

Before I wrap up, I'll just show you an example of the kind of interesting stuff that you can do by doing this kind of exercise.

Remember earlier I mentioned that one of our alumni who works at Splunk which is a NASDAQ listed big successful company created this new anti-fraud software. This is actually how he created it as part of a fastai part 1 class project:

![](../../../../images/fastai_p1_v3/lesson_1/132.jpg)

He took the telemetry of users who had Splunk analytics installed and watched their mouse movements and he created pictures of the mouse movements. He converted speed into color and right and left clicks into splotches. He then took the exact code that we saw with an earlier version of the software and trained a CNN in exactly the same way we saw and used that to train his fraud model. So he **took something which is not obviously a picture and he turned it into a picture** and got these fantastically good results for a piece of fraud analysis software.

So it pays to think creatively. So if you are wanting to study sounds, a lot of people that study sounds do it by actually creating a spectrogram image and then sticking that into a ConvNet. So there's a lot of cool stuff you can do with this.

So during the week, get your GPU going, try and use your first notebook, make sure that you can use lesson 1 and work through it. Then see if you can repeat the process on your own dataset. Get on the forum and tell us any little success you had. Any constraints you hit, try it for an hour or two but if you get stuck, please ask. If you are able to successfully build a model with a new dataset, let us know! I will see you next week.

:warning::warning::warning:Don't forget to shutdown your GPU instance so that you don't keep getting charged!:warning::warning::warning:
