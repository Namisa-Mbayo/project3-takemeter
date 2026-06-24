## Community:

The community I chose was the reality TV show, Real Housewives. They have a very active and opinionated fanbase where people constantly debate over cast behavior, episode events, and relationships. They go through a variety of discussion points, from posts about simple recaps of episodes to deep arguments about motives and intentions.

## Label Taxonomy

| Label | Definition | Examples |
| - | - | - |
| `show_reaction` | A post that expresses an emotional response or personal feeling about something that happened in the show. | “This scene stressed me out.” / “That dinner scene was absolute chaos. I had to rewind.” |
| `character_judgment` | A post that evaluates a cast member’s personality, motives, morality, likability, or behavior. | “She only apologized because she knew the cameras were on her.” / “He’s trying way too hard to look like the reasonable one this season.” |
| `storyline_analysis` | A post that explains a take using specific evidence from episodes/seasons, editing choices, production framing, or social dynamics. | “The edit has been setting her up as the villain for weeks by cutting from her confessionals directly into the other women reacting negatively.” / “This conflict feels less about the dinner argument and more about the alliance shift that started after the cast trip.” |
| `fandom_commentary` | A post that discusses the subreddit, Bravo fandom, viewer behavior, stan wars, or how viewers talk about the show. | “Fans don’t know what they want.” / “My biggest housewives gripe are scenes in the trailer and previews for the next episode that NEVER GET SHOWN.” |

**Decision rule:** If the post  expresses a feeling about a scene, episode, reunion, trailer, or on-screen moment, label it `show_reaction`. If the post makes an evaluative claim about a cast member's actions, personality, or other traits, label it `character_judgment`. If the post mainly explains why something happened, how a dynamic works, or how editing choices/storyline context influence how viewers understand events, label it `storyline_analysis`. The post may include opinions, but the main purpose is interpretation. If the post talks about the audience, subreddit, or Bravo fandom, label it `fandom_commentary`. When multiple labels seem possible, choose the label that best describes the post’s main purpose.

## Hardest Edge Cases

The hardest edge case will be `character_judgment` vs. `analysis`   
*Example:* “She only apologized because she knew the cameras were on her.”   
This could be labeled `character_judgment` because it evaluates the cast member’s sincerity and motives. However, if the post expands on that claim using specific scenes, behavior, editing choices, or group dynamics, it should become `storyline_analysis`.

A second possible edge case is `show_reaction` vs. `character_judgment`. If a post mostly reacts to a moment, label it `show_reaction`. If it uses that moment to evaluate a cast member’s personality or motives, label it `character_judgment`.

## Data Collection Plan

I will collect examples from the Real Housewives Reddit community, r/BravoRealHousewives. I will collect posts and comments from various discussion threads, collecting at least 200 examples total. Since I have 4 labels, I will aim for about 50 examples per label. If one label is underrepresented, I will search for threads where that label is more common.

## Evaluation Metrics

I will evaluate both the fine-tuned model and the zero-shot baseline on the test set. I will report:

- Overall accuracy
- Per-class precision, recall, and F1 score
- Confusion matrix

Accuracy alone is not enough because the dataset may be imbalanced, or one label may be easier to classify than the others. Per-class metrics are important because the model might perform well overall while still failing a specific label. The confusion matrix will show which labels are being confused with each other. This is especially important for my edge cases since I expect errors between `character_judgment` and `storyline_analysis`.

## Definition of Success

A useful classifier should perform better than the zero-shot baseline on the same test set. I would consider the model successful if:

- The fine-tuned model beats the zero-shot baseline in overall accuracy.
- Each label has an F1 score of at least 0.60.
- The model predicts all labels.
- Most mistakes are reasonable edge cases.

I wouldn't deploy this as a real community tool yet. The model needs better performance, more labeled data, clearer  guidelines, and human review for uncertain prediction.

## AI Tool Plan

**Label stress-testing:** 
I will use Claude to stress-test my label taxonomy before annotating the full dataset. I will provide my label definitions, examples, and edge case description, then ask it to generate 5-10 Real Housewives posts that could fit between two labels (`character_judgment` and `storyline_analysis`). If I cannot clearly classify those examples, I will revise my definitions before labeling.

**Failure analysis:**
After evaluating the fine-tuned model, I will give Claude a list of wrong predictions, including the text, true label, and predicted label. I will ask it to identify error patterns, such as whether the model confuses emotional but evidence-based posts with `character_judgment`. I will verify any patterns myself by rereading the examples and comparing them to my label definitions. The AI tool will brainstorm failure patterns, but I will make the final decision.
