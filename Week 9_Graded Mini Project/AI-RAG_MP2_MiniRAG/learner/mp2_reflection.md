# MP2 Reflection

## What worked
Splitting on paragraphs and treating short lines with no full stop as section headers. Every chunk got a section name for free, so citations came out as "The Speckled Band - The Ventilator" instead of chunk 37. Made it easy to see if retrieval was in the right part of the story. Both predefined questions cited the right file (2/2).

## What didn't work
q1 asks who the assistant was and what his real identity was. The chunk with the answer says "Holmes recognises Spaulding as John Clay, the grandson of a royal duke..." but it never uses the words assistant, pawnshop, Wilson or identity. So the embedding didn't match the question and it was not even in the top 8. The section got split into two chunks (345 + 323 chars, over the 500 limit together) and only the tunnelling half got retrieved. The LLM said Vincent Spaulding, explained the tunnel, never said John Clay. Right story, 1/5 facts. Bumping k from 3 to 5 did not fix it.

## What I'd change
Embed title + section + text instead of just the text. The section header is literally "The Identity of the Assistant" - the exact words in the question. I was already storing it in the payload for citations, just not using it for search. Also raise TARGET_CHUNK_SIZE to around 700 so a short 2 paragraph section stays as one chunk.

## One surprise
The script crashed before any RAG code ran. print("→ Loading corpus…") failed with UnicodeEncodeError because PowerShell gives Python a cp1252 console. PYTHONUTF8=1 fixed it, but I spent time thinking the pipeline was broken when it never started.

The other one - the q1 miss looked like a case for hybrid search (question says assistant, chunk says Spaulding). But BM25 would not have helped either, the word is just not in the chunk. Only the section header connects the two.
