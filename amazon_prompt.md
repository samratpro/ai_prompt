## Title
```
Write an SEO title about this keyword within 55 characters. The keyword must be included directly in the title keyword: ((keyword))
rules:
1. Never mention year
2. Must be within 55 characters
3. Must be clickbait
```
## Intro
```
Write a compelling blog post introduction about the keyword: ((keyword)) 
The introduction should begin with technical terms related to the topic, avoiding casual phrases like "Are you...". The keyword should be naturally included throughout the introduction. Do not provide a direct solution in the intro. 
The final sentence should intrigue readers to continue reading the full article. Aim for a length of approximately 120 words. 
```
## H2
```
Write an sub title on this keyword, this title will insert before a production comparison list : ((keyword))
rules:
1. Must be interesting
2. Never directly place keyword
```
## Product
```
Write a detailed and structured product description for the following product in the format provided below.
**Product Details:**
- Focus Keyword: ((keyword)) [Only for intention]
- Product Link: ((link))
- Product Title: ((title))
- Product  Description: ((description))
- Technical Data: ((technical_data))
- User Review: ((review))
- Price: ((price))

**Requirements:**
1. Start with a compelling introduction highlighting the product’s main appeal.
2. Format the output in clean HTML with WordPress-compatible tags.
3. Avoid repetitive phrasing (e.g., no overuse of "this toy" or "this product" to start sentences).
4. Emphasize unique features and benefits in a structured format:
<p> {{Engaging start, and Detailed product description with features within 150 words}} </p>
<h3>Pros</h3>
<ul>
    <li>{{Benefit 1}}</li>
    <li>{{Benefit 2}}</li>
    <li>{{Benefit 3}}</li>
</ul>
<h3>Cons</h3>
<ul>
    <li>{{Drawback 1}}</li>
</ul>
<p> {{Concise closing statement reinforcing value.}} </p>
5. Tone should be informative and consumer-focused, avoiding fluff while delivering value.
6. If applicable, briefly compare it with similar products to enhance the reader’s decision-making.
7. Ensure proper sentence variation to prevent repetition while maintaining clarity.
8. Omit ```html``` label
```
## Buying Guide H2
```
Write an buying guide title for this keyword: ((keyword))
1. Never mention year
2. Must be interesting
```
## Buying Outline
```
Generate an outline for an buying guide outline for this keyword: ((keyword)) [what to consider before purchase a product]
The outline consists of multiple H2's with briefing.
Only an outline needed, do not give answers, unnecessary words or notes. Do not give me "Overview", "Introduction" or "Conclusion" etc. others
The outline should have the following format, between 6 to 8, H2 section:
<h2></h2>
  - subtopic
  - subtopic
  - subtopic
   <!-- Add as many points as needed -->
<h2></h2>
   - subtopic
   - subtopic
   - subtopic
    <!-- Add as many points as needed -->
<h2></h2>
    <!-- Add as many heading and points as needed -->
```
## Buying Paragraph
```
Write a buying guide paragraph explaining why it is important to consider Connectivity and Expansion before purchasing a ((keyword)). Ensure all sentences are meaningful and written in a natural, native style.
**Instructions:**  
1. **Do not** start the paragraph with the heading name.  
2. **Must avoid** using the phrases:  
   - "when considering"  
   - "choosing"  
   - "selecting"  
   - "looking"  
   - "seeking"  
   - "searching"
   - "purchasing"
   - "buying"
   - "purchasing"
   - "buying"
   - "Connectivity" 
   - "Expansion" 
   - "((keyword)) " (do not include this in output).  
   - "what to consider before purchase a product" (do not include this in output).
   - The exact words: **"Connectivity" and "Expansion"**  
3. **Start directly with an informative fact** instead of general advice.  
4. **Maintain a structured format** covering all given topics.  
5. Enhance readability with <p>, <strong>, <ul>, and <table> tags where appropriate. Use a <table> only when presenting structured comparisons, multiple data rows, pros vs. cons, or one topic vs. another. Avoid adding tables for simple lists or single-topic explanations.

**Details:**  
- **Keyword (for reference only, do not include in the output):** ((keyword))
- **Paragraph Heading:** ((heading))
- **Topics to Cover:**  
((topic_to_cover))
```
## FAQ
```
Topic: ((keyword))
Write 5 related questions on this topic
1.
```
## FAQ Ans
```
Instruction: Answer the following question concisely in exactly two sentences without introductory phrases like “Here is your answer” or “Regarding your question.” Provide a direct and informative response.
Question: ((question))
```
## Conclusion
```
keyword: ((keyword)) Write an web article bottom summary and length approx. 60 words
```

## paragraph_format
```py
def paragraph_format(text_for_format):
    def text_format(text):
        p_format = re.split(r'([?.!])', text.replace("<p>", "").replace("</p>", ""))
        p_format = [p_format[i] + p_format[i + 1] for i in range(0, len(p_format) - 1, 2)]
        paragraphs = [''.join(p_format[:choice([2, 3])]), ''.join(p_format[choice([2, 3]):5]),
                      ''.join(p_format[5:choice([7, 8])]), ''.join(p_format[choice([7, 8]):10]), ''.join(p_format[10:])]
        wp_paragraphs = ''.join(f'<!-- wp:paragraph --><p>{p}</p><!-- /wp:paragraph -->' for p in paragraphs if p)
        text = re.sub(r'\s{2,}', ' ', wp_paragraphs)
        text = re.sub(r'<!-- wp:paragraph --><p></p><!-- /wp:paragraph -->', '', text)
        text = re.sub(r'<p>\s+', '<p>', text)
        text = re.sub(r'\n', '', text)
        text = re.sub(r'\b\d+\.', '', text)
        return text.replace('"', '').replace("*", "")

    paragraph = ""
    splited = text_for_format.replace('<p>', '---<p>').replace('<h2>', '---<h2>').replace('<h3>', '---<h3>').replace(
        '<ul>', '---<ul>').replace('<table>', '---<table>').replace('</p>', '</p>---').replace('</h2>',
                                                                                               '</h2>---').replace(
        '</h3>', '</h3>---').replace('</ul>', '</ul>---').replace('</table>', '</table>---').strip().split(sep='---')
    for element_part in splited:
        if "<h2>" in element_part:
            formated = '<!-- wp:heading -->' + element_part + '<!-- /wp:heading -->'
        elif "<h3>" in element_part:
            formated = '<!-- wp:heading {"level":3} -->' + element_part + '<!-- /wp:heading -->'
        elif "<ul>" in element_part:
            formated = '<!-- wp:list -->' + element_part + '<!-- /wp:list -->'
        elif "<table>" in element_part:
            formated = '<!-- wp:table {"hasFixedLayout":false,"className":"is-style-stripes"} --><figure class="wp-block-table is-style-stripes">' + element_part.replace(
                "\n", "") + '</figure><!-- /wp:table -->'
        elif "<p>" in element_part:
            formated = text_format(element_part)
        else:
            formated = text_format(element_part)
        if formated != "":
            paragraph += formated
    return paragraph
```



