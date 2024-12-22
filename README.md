# ai_prompt
### 01. Title
```py
title_prompt = '''Write an SEO title about this keyword within 55 characters. The keyword must be included directly in the title
keyword: <<keyword>>
'''
```
```py
outline_prompt = '''
Generate an outline for an article that can cover all relevant topics on the keyword: <<keyword>>
The outline consists of one H1 heading and multiple H2's with briefing.
Only an outline needed, do not give answers, unnecessary words or notes. Do not give me "Overview", "Introduction" or "Conclusion" etc. others
The outline should have the following format, between 8 to12, H2 section:
<H1></H1>
<h2></h2>
- subtopic
- subtopic
- subtopic
- subtopic
<h2></h2>
- subtopic
- subtopic
- subtopic
- subtopic
<h2></h2>
- subtopic
- subtopic
- subtopic
- subtopic
<h2></h2>
.........
'''
```
### 03. introduction_prompt
```py
introduction_prompt = '''Write a compelling blog post introduction about the keyword: <<keyword>>
The introduction should begin with technical terms related to the topic, avoiding casual phrases like "Are you...". The keyword should be naturally included throughout the introduction. Do not provide a direct solution in the intro. The final sentence should intrigue readers to continue reading the full article. Aim for a length of approximately 120 words.
```
### 04. paragraph_prompt
```py
paragraph_prompt = '''Write this section for the mentioned paragraph heading within 120 words so that it is useful for the reader, in an interesting and organized way like human writing. Each output sentence will be short, meaningful and native.
Also on important points you can add <em></em> if necessary.
the article keyword of this paragraph is <<keyword>> (The keyword only informs you about my main point, just remember it),
paragraph heading is: <<heading>>
The topic you followed <<topic_to_cover>>

You can add bullets or tables in sections if appropriate. Bullets and tables with <ul><li> tags, <em></em> tags, <table></table> tags and paragraphs with <p></p> tags. However, try to avoid the table tag if it is not up to 60% necessary. Do not start the sentence with the exact name of the heading or do not start with the heading and the context of the keyword base.
'''
```
### 05. conclusion_prompt
```py
conclusion_prompt = """Write a conclusion for this keyword that you will use in the final conclusion of the content, in 100 words or less.
Keyword: <<keyword>>
"""
```
### 06. excerpt_propt
```py
excerpt_propt = '''Write a short summary,
Keyword: <<keyword>>,
Must include keyword in output
and length approx. 20 words
'''
```
