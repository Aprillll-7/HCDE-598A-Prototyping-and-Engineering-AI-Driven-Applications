# Exercise Prompt

<Hard>

Explore 1.3: The API specification allows us to send parameters in the request body that will change how the LLM model generates text. These parameters would become part of the `chat_context` that we send in the request. Two valuable parameters to explore are temperature and max_completion_tokens. Modify the code to include two new constants called `OAI_MODEL_TEMPERATURE` and `OAI_MODEL_MAX_TOKENS`. Then modify the `new_chat_context()` function to include the temperature and max_completion_tokens parameters and set them to the respective constants. Review the Open API documentation to understand how responses change as you change the temperature and max_completion_tokens parameters.

# Modification

1. Add new constants:
    
    ```python
    #   Include temperature and max completion tokens
    OAI_MODEL_TEMPERATURE = 0.3
    OAI_MODEL_MAX_TOKENS = 300
    ```
    
    For temperature, higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic.
    
    For max tokens, it refers to an upper bound for the number of tokens that can be generated for a completion, including visible output tokens and reasoning tokens.
    
    For more details, refer to the [OpenAI API Reference Documentation](https://platform.openai.com/docs/api-reference/chat/create).
    
2. Update `new_chat_context()` to include these:
    
    ```python
    def new_chat_context():
        chat_context = dict()
        chat_context['model'] = OAI_MODEL
        chat_context['messages'] = list()
        system_turn = new_chat_turn("system",MOVIE_RECOMMENDER_PERSONA_PROMPT)
        chat_context['messages'].append(system_turn)
        chat_context['temperature'] = OAI_MODEL_TEMPERATURE
        chat_context['max_completion_tokens'] = OAI_MODEL_MAX_TOKENS
        return chat_context
    ```
    

# Example Output

1. When the `OAI_MODEL_TEMPERATURE` is 0.3:
    
    User prompt > I want to see a movie with my friend this weekend. We are thinking of watching it at home. Do you have any good recommendations?
    
    > Certainly! To give you the best recommendation, could you share a bit more about your preferences? For instance, what genres do you and your friend enjoy? Are there any specific actors or directors you're fans of? Do you prefer recent releases or are classics also on the table? Any particular mood or themes you're aiming for? This information will help tailor a suggestion that you both will enjoy.
    
    User prompt > Emmm we both share a deep love for movies and could be picky. I wouldn't say there is a specific genre we enjoy, but I do want to watch something that is thought-provoking while engaging. Classics are fun but no cliche stuff--we might have watched them already.
    
    > Given your interest in thought-provoking and engaging movies that steer clear of clichés, I recommend exploring films that blend deep narratives with innovative storytelling. Here are a few suggestions across different genres and eras, each known for its unique approach, compelling plots, and rich character development:
    > 1. **"Eternal Sunshine of the Spotless Mind" (2004)** - Directed by Michel Gondry and written by Charlie Kaufman, this film blends elements of science fiction with a profound romantic narrative. It explores the complexities of relationships and the human psyche through a visually stunning and unconventional storyline.
    > 
    > 2. **"Inception" (2010)** - Directed by Christopher Nolan, this sci-fi thriller delves into the intricacies of dreams within dreams. With its groundbreaking visuals and a plot that challenges viewers to unravel its complexities, it's a film that sparks discussions long after the credits roll.
    > 3. **"Pan's Labyrinth" (2006)** - Directed by Guillermo del Toro, this Spanish-language film combines historical fiction with fantasy, set against the backdrop of post-Civil War Spain. It's a visually captivating, dark fairy tale that explores themes of innocence, brutality, and escapism.
    > 4. **"Her" (2013)** - Directed by Spike Jonze, this sci-fi drama explores the nature of love and loneliness in the not-so-distant future. It's a poignant examination of human relationships and technology, featuring a compelling narrative and strong performances.
    > 5. **
    
2. When the `OAI_MODEL_TEMPERATURE` is 0.8:
    
    User prompt > I want to see a movie with my friend this weekend. We are thinking of watching it at home. Do you have any good recommendations?
    
    > Absolutely, I'd be happy to help! To provide you with the best recommendation, I need a bit more information. Are there any specific genres you and your friend enjoy? Are you looking for something recent, or are classics also on the table? Any favorite actors or filmmakers? And lastly, what kind of mood are you aiming for—something light and funny, thrilling and intense, or maybe deeply emotional and thought-provoking?
    
    User prompt > Emmm we both share a deep love for movies and could be picky. I wouldn't say there is a specific genre we enjoy, but I do want to watch something that is thought-provoking while engaging. Classics are fun but no cliche stuff--we might have watched them already.
    
    > Given your interest in thought-provoking and engaging films without delving into the too-familiar territories of clichés, I'd recommend exploring a couple of exceptional movies that stand out for their uniqueness, depth, and engaging storytelling. These recommendations should cater to a broad taste while ensuring you're both captivated and intellectually stimulated:
    >
    > 1. **"Eternal Sunshine of the Spotless Mind" (2004)** - Directed by Michel Gondry and written by Charlie Kaufman, this film blends elements of science fiction with a deeply emotional love story. It's visually inventive and structurally complex, exploring the nature of memory and love. The performances by Jim Carrey and Kate Winslet are exceptional, and the film's unique approach to its narrative ensures it's anything but cliché.
    > 
    > 2. **"Pan's Labyrinth" (2006)** - Directed by Guillermo del Toro, this Spanish language film is a dark fairy tale set against the post-Civil War era in Spain. It combines historical drama with fantasy in a way that's both visually stunning and narratively captivating. The story is deeply allegorical, filled with rich symbolism that engages with themes of innocence, fascism, and the power of imagination.
    > 
    > 3. **"Arrival" (2016)** - Directed by Denis Villeneuve, this film offers a fresh take on the alien invasion genre. Focused more on linguistics, communication, and the human condition rather than interstellar conflict. It's a visually stunning, intellectually

Interestingly under both condition, *Pan's Labyrith* and *Eternal Sunshine of the Spotless Mind* were recommended. 
