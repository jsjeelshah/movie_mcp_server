
#  Movie Rating MCP Server

This project implements a MCP-style microservice that uses a Large Language Model (LLM) and [The Movie Database (TMDb)](https://www.themoviedb.org/) API to return the star rating, overview, and metadata for a given movie.

Example prompts:

* “What was the rating for Rounders?”
* “What was the rating for that Matt Damon poker movie?”
* “What was the rating for the poker movie starring Ed Norton and John Malkovich?”



##  Features

- Uses FastAPI to expose an MCP-style HTTP endpoint
- Integrates LLM (via `g4f`) to interpret movie names from natural language
- Fetches real-time movie details from TMDb API
- Returns clean, structured JSON responses
- Can be tested directly from a Jupyter Notebook or local browser

---

##  How It Works

1. **User Query → LLM Extraction**

   * The LLM parses your query to extract the likely movie title.
   * Example:
     Input: “What was the rating for that Matt Damon poker movie?”
     LLM Output: `{"title": "Rounders"}`

2. **TMDb Search → Movie Data Fetch**

   * The server queries TMDb’s `/search/movie` and `/genre/movie/list` endpoints to retrieve the top matching movie and its details.

3. **Response → JSON Output**

   * Returns movie title, rating, overview, release year, and genres in structured format.



##  Project Structure

```
movie_mcp.ipynb    # Jupyter notebook running FastAPI locally
```

---

##  Setup Instructions

###  Clone the Repository

```bash
git clone https://github.com/jsjeelshah/movie_mcp_server.git
cd movie_mcp_server
```

###  Install Dependencies

Make sure Python 3.10+ is installed, then run:

```bash
pip install fastapi nest_asyncio httpx pydantic g4f uvicorn
```



##  Running the Server (Inside Jupyter)

Simply run all cells in the notebook.

The FastAPI server will start on:

```
http://127.0.0.1:8002
```

---

##  Example Usage

Once the server is running, open your browser or use `curl` to query:

```bash
http://127.0.0.1:8002/movie?query=What+was+the+rating+for+Avatar%3F
```

### Example Output

```json
{
  "title": "Avatar",
  "rating": 7.6,
  "overview": "In the 22nd century, a paraplegic Marine is dispatched to the moon Pandora...",
  "release_year": 2009,
  "genres": ["Action", "Adventure", "Science Fiction"]
}
```

You can also modify the `queries` list inside the notebook to test multiple prompts automatically.

---

##  Example Queries Tested

| Query                                                                            | Expected Movie |
| -------------------------------------------------------------------------------- | -------------- |
| “What was the rating for Avatar?”                                                | Avatar         |
| “What was the rating for that Matt Damon poker movie?”                           | Rounders       |
| “What was the rating for Inception?”                                             | Inception      |
| “What was the rating for the poker movie starring Ed Norton and John Malkovich?” | Rounders       |



##  Design Choices & Reasoning

* **FastAPI** → lightweight, async, and perfect for MCP-style endpoints.
* **LLM (g4f)** → interprets vague or indirect natural language references.
* **TMDb API** → provides real, reliable movie data.
* **nest_asyncio** → enables running `uvicorn` inside Jupyter for quick demos.
* **Pydantic** → defines structured response models and ensures clean API responses.




##  Summary

This project demonstrates a **functional MCP microservice** that connects **LLM understanding** with a **real-world data API** to answer complex, natural language questions about movies.
It showcases clean design, modular structure, and readiness for integration with a downstream **AI agent**.

