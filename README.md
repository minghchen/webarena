# WebArena: A Realistic Web Environment for Building Autonomous Agents
<p align="center">
    <img src="media/logo.png" alt="Logo" width="80px">
    <br>
    <b>WebArena is a standalone, self-hostable web environment for building autonomous agents</b>
</p>


<p align="center">
<a href="https://www.python.org/downloads/release/python-3109/"><img src="https://img.shields.io/badge/python-3.10-blue.svg" alt="Python 3.10"></a>
<a href="https://pre-commit.com/"><img src="https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white" alt="pre-commit"></a>
<a href="https://github.com/psf/black"><img src="https://img.shields.io/badge/code%20style-black-000000.svg" alt="Code style: black"></a>
<a href="https://mypy-lang.org/"><img src="https://www.mypy-lang.org/static/mypy_badge.svg" alt="Checked with mypy"></a>
<a href="https://beartype.readthedocs.io"><img src="https://raw.githubusercontent.com/beartype/beartype-assets/main/badge/bear-ified.svg" alt="bear-ified"></a>
</p>

<p align="center">
<a href="https://webarena.dev/">Website</a> •
<a href="https://arxiv.org/abs/2307.13854">Paper</a> •
<a href="https://docs.google.com/spreadsheets/d/1M801lEpBbKSNwP-vDBkC_pF7LdyGU1f_ufZb_NWNBZQ/edit?usp=sharing">Leaderboard</a>
</p>

![Overview](media/overview.png)

## Notice

Here is the branch of **[WebArena](https://github.com/web-arena-x/webarena)** used in **[AutoManual](https://arxiv.org/abs/2405.16247)**. We have made the following **corrections and improvements** to the original WebArena so that LLM Agents can obtain correct information:

1. After each action is executed, an additional "none_action" is executed, to ensure that the action has been completed.
2. The scroll bar information of the web page is added to the observation, to indicate the location of the current visible area.
3. When a focused element has a property of "hasPopup", its current value and options in the popup menu will be displayed. (Fix the [issue](https://github.com/web-arena-x/webarena/issues/121) that the original env cannot display the content in the popup menu)
4. Add "select" action for id-based actions, allowing the agent to select an option in a popup menu.
5. Add "fill" action for id-based actions, allowing the agent to clear existing content before type.
6. Fix the [issue](https://github.com/web-arena-x/webarena/issues/139) of fuzzy match a list.

To facilitate comparison with the original branch, we added a comment starting with "# [cmh]:" to each modified code.



**We also fixed some annotation issues.** (We will continue to update more annotation issues)

Reddit:

- task_id 28: "Tell me the count of comments that have received more downvotes than upvotes for the user who made the latest post on the Worcester forum." The answer should be 1 instead of 0
- task_id 407, 408: "Upvote the newest post in deeplearning subreddit" The original answer checked the hottest post instead of the latest post
- task_id 583: "Create a new forum named PlantsForCatParents, with a description of Cat parents & plan lovers, and include ['Cat friendly', 'Local vendors', 'Promotion', 'Toxic plants!'] in the sidebar?" It should be "plant lovers" instead of "plan lovers"
- task_id 584: "Create a new forum named Karaoke, with a description of Place for Karaoke lovers, and include ['devices', 'setup'] in the sidebar?" The URL in the answer check should be changed to `"__REDDIT__/f/Karaoke/edit"` instead of `"__REDDIT__/f/Karaoke"`.
- task_id 603, 608: "Post my question, \"safe and budge apartment to live in nyc\", in a subreddit where I'm likely to get an answer" in which "budge apartment" should be "budget apartment"
- task_id 644: "Post a notice on a virtual meetup for Tears of Kingdom enthusiasts on Dec 15th in the games subreddit" There is only a "gaming" subreddit in the environment, not a "games" subreddit



## Install
```bash
# Python 3.10+
conda create -n webarena python=3.10; conda activate webarena
pip install -r requirements.txt
playwright install
pip install -e .
```

Then setup the standalone environment. Please check out [this page](environment_docker/README.md) for details.


> [!IMPORTANT]
> After evaluating the 812 examples, reset the environment to the initial state following the instructions [here](./environment_docker/README.md#environment-reset).

Configurate the urls for each website by setting your [AWS hostname](./environment_docker/README.md#Pre-installed Amazon Machine Image).

```bash
export AWS_HOSTNAME="<your-server-hostname>"

export OPENAI_API_KEY="<your-api-key>" # a valid OpenAI API key starts with sk-
export OPENAI_BASE_URL="<your-base-url>" # e.g., https://api.openai.com/v1
```



## Citation

If you use the environment or data, please cite the paper:
```
@article{zhou2023webarena,
  title={WebArena: A Realistic Web Environment for Building Autonomous Agents},
  author={Zhou, Shuyan and Xu, Frank F and Zhu, Hao and Zhou, Xuhui and Lo, Robert and Sridhar, Abishek and Cheng, Xianyi and Bisk, Yonatan and Fried, Daniel and Alon, Uri and others},
  journal={arXiv preprint arXiv:2307.13854},
  year={2023}
}
```
