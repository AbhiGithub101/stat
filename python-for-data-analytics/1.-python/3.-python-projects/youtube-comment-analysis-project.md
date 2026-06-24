# YouTube Comment Analysis Project



{% file src="../../../.gitbook/assets/comments_file" %}

<details>

<summary>Project Code </summary>

```python
# Read comments from file
file = open("comments_file", "r")

comments = file.readlines()

file.close()

# Remove new line characters

clean_comments = []

for comment in comments:
    clean_comments.append(comment.strip())

comments = clean_comments

# Total Comments

total_comments = len(comments)

# Positive and Negative Words

positive_words = [
    "amazing",
    "helpful",
    "excellent",
    "great",
    "awesome",
    "thanks",
    "good",
    "best"
]

negative_words = [
    "bad",
    "worst",
    "poor",
    "not",
    "useless",
    "boring"
]

# Sentiment Analysis

positive_count = 0
negative_count = 0
neutral_count = 0

for comment in comments:

    words = comment.lower().split()

    positive_score = 0
    negative_score = 0

    for word in words:

        if word in positive_words:
            positive_score = positive_score + 1

        elif word in negative_words:
            negative_score = negative_score + 1

    if positive_score > negative_score:
        positive_count = positive_count + 1

    elif negative_score > positive_score:
        negative_count = negative_count + 1

    else:
        neutral_count = neutral_count + 1


# Word Frequency Analysis

word_frequency = {}

for comment in comments:

    words = comment.lower().split()

    for word in words:

        if word in word_frequency:
            word_frequency[word] = word_frequency[word] + 1

        else:
            word_frequency[word] = 1

# Most Frequent Word

max_count = 0
most_frequent_word = ""

for word in word_frequency:

    if word_frequency[word] > max_count:

        max_count = word_frequency[word]
        most_frequent_word = word

# Longest Comment

longest_comment = comments[0]

for comment in comments:

    if len(comment) > len(longest_comment):
        longest_comment = comment

# Shortest Comment

shortest_comment = comments[0]

for comment in comments:

    if len(comment) < len(shortest_comment):
        shortest_comment = comment

# Average Words Per Comment

total_words = 0

for comment in comments:

    words = comment.split()

    total_words = total_words + len(words)

average_words = total_words / total_comments

# Overall Remark

if positive_count > negative_count:
    overall_remark = "Video is performing well. Most viewers have a positive opinion."

elif negative_count > positive_count:
    overall_remark = "Video needs improvement. Many viewers have a negative opinion."

else:
    overall_remark = "Viewers have mixed opinions about the video."

# Display Report

print()
print("=" * 50)
print("YOUTUBE COMMENT ANALYSIS REPORT")
print("=" * 50)

print("Total Comments :", total_comments)
print("Positive Comments :", positive_count)
print("Negative Comments :", negative_count)
print("Neutral Comments :", neutral_count)

print()
print("Most Frequent Word :", most_frequent_word)

print()
print("Longest Comment :")
print(longest_comment)

print()
print("Shortest Comment :")
print(shortest_comment)

print()
print("Average Words Per Comment :", round(average_words, 2))

print()
print("Word Frequency Analysis")

for word in word_frequency:
    print(word, ":", word_frequency[word])

print()
print("Overall Remark :")
print(overall_remark)

print("=" * 50)
```

</details>
