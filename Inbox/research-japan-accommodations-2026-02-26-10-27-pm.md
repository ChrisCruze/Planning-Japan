# Input


### Prompt to paste into ChatGPT / Claude / other LLM

You are a research assistant specialized in places in Tokyo, Japan.  
Follow these instructions exactly and return all results in English.

I will give you either a single place or a list of places, all intended to be within Tokyo, Japan.

For EACH place I give you, do ALL of the following:

1. Confirm it is in Tokyo, Japan.  
- If it does not appear to be in Tokyo, Japan, set `"in_tokyo": false` for that place and fill other fields with `null` or a short explanation string where appropriate.

1. If it is in Tokyo, Japan, find and output:
- Name of the place (as commonly written in English)
- Full address (including ward, Tokyo, and postal code if available)
- Latitude and longitude in decimal degrees
- Google Maps link to the exact place
- Official website URL (if none exists, use the string `"No official website found"`)

1. Create a short content block with:
- A catchy headline (max 12 words)
- A 2–3 sentence summary focusing on what this place is
- A 2–4 sentence description that adds a bit more color or context

1. Calculate the **straight-line distance** in kilometers from this hotel:  
   Nest Hotel Tokyo Hanzomon  
   Address: 2-18 Hayabusacho, Chiyoda City, Tokyo 102-0092, Japan  
   Approx. coordinates: 35.6818° N, 139.7410° E  
- Use the given coordinates for the hotel.  
- Use the best available coordinates you find for the place.  
- Round the final distance to one decimal place.  
- If you cannot get coordinates for the place, use `null` for the distance and the string `"Distance unavailable (no coordinates)"` in an explanation field.

1. Return your final answer **only** as a JSON array of objects (no extra text before or after the JSON).  
   Each place must be one object using this exact schema:

```
[
  {
    "input_place_raw": "",
    "in_tokyo": true,
    "place_name": "",
    "place_address": "",
    "place_latitude": 0,
    "place_longitude": 0,
    "google_maps_link": "",
    "official_website": "",
    "headline": "",
    "summary": "",
    "description": "",
    "distance_from_nest_hotel_tokyo_hanzomon_km": 0.0,
    "distance_note": ""
  }
]
```

- `input_place_raw`: Exactly what I typed for that place.
- `in_tokyo`: Boolean, whether you judge this place to be in Tokyo, Japan.
- `distance_note`:  
- Use `""` (empty string) if the distance was calculated normally.  
- Use a brief explanation like `"Distance unavailable (no coordinates)"` or `"Place not in Tokyo"` if needed.

Now wait for my input. I will provide either:
- a single place, like: `Tokyo Skytree`  
- or multiple places separated by new lines, like:  
  `Tokyo Skytree`  
  `Shinjuku Gyoen National Garden`  
  `teamLab Planets TOKYO`

For whatever I send next, process it using the rules above and output only the JSON array.

\*\*\*

If you want, I can also add an option in the prompt to include step‑by‑step transit directions from the hotel (e.g., subway route and approximate time).

Sources
[1] Nest Hotel Tokyo Hanzomon - Google https://www.google.com.kw/travel/hotels/entity/ChkIw8Xfl7vSm_QLGg0vZy8xMWhjdnc3bTM0EAE?ap=MABIAVp1CgQIPBAAIgNLV0QqFgoHCOIPEAwYCxIHCOIPEAwYDBgBKAByAggCigEoChIJ58hMsQ_dQUARH0cLMI12YUASEgltpW8PPd5BQBH5SB4ezHZhQJIBAiABmgEHEgVUb2t5b6IBEQoIL20vMDdkZmsSBVRva3lv&g2lb=4181926%2C4208993%2C4209588%2C4207631%2C4215556%2C4219394%2C4220469&hl=en&un=0&rp=OAFAAEgCwgIcIhoNAAAAQRITCMLIkLjjjpADFe4s1AEdoVAgtA&ictx=1&sa=X&tcfs=EisKCC9tLzA3ZGZrEgVUb2t5bxoYCgoyMDE4LTEyLTExEgoyMDE4LTEyLTEyGAJSAA&ts=CAEaBAoCGgAqBAoAGgA&ei=4dWVabnFJN_olsYPxcWtuAU&ei=O9-VaajbDY_klsYPqfS72Q4&ved=2ahUKEwjo5PXrseOSAxUPssUCHSn6LusQkdkIegUIBBDYAQ
[2] Nest Hotel Tokyo Hanzomon - Booking.com https://www.booking.com/hotel/jp/nesutohoterudong-jing-ban-zang-men.html
[3] Nest Hotel Tokyo Hanzomon Reviews, Deals & Photos 2026 - Expedia https://www.expedia.com/Tokyo-Hotels-NEST-HOTEL-TOKYO-HANZOMON.h20577231.Hotel-Information
[4] It was fine, I guess. - Review of Nest Hotel Tokyo Hanzomon ... https://www.tripadvisor.com/ShowUserReviews-g1066443-d13284153-r945665377-Nest_Hotel_Tokyo_Hanzomon-Chiyoda_Tokyo_Tokyo_Prefecture\_Kanto.html
[5] Nest Hotel Tokyo Hanzomon - Skyscanner https://www.skyscanner.net/hotels/japan/tokyo-hotels/nest-hotel-tokyo-hanzomon/ht-160961870
[6] NESTHOTEL TOKYO HANZOMON https://www.nesthotel.co.jp/tokyohanzomon/en/
[7] Nest Hotel Tokyo Hanzomon https://www.hotels-tokyo-jp.net/en/property/nest-hotelhanzomon/location.html
[8] Nest Hotel Tokyo Hanzomon, Japan - www.trivago.com https://www.trivago.com/en-US/oar/nest-hotel-tokyo-hanzomon?search=100-8758034
[9] Japan - NEST HOTEL TOKYO HANZOMON https://nest-hanzomon.intokyohotels.com/en/
[10] NEST HOTEL TOKYO HANZOMON - Prices & Reviews (Japan) https://www.tripadvisor.com/Hotel_Review-g1066443-d13284153-Reviews-Nest_Hotel_Tokyo_Hanzomon-Chiyoda_Tokyo_Tokyo_Prefecture_Kanto.html
[11] Hotel Monterey Hanzomon - Tokyo - Travel Weekly https://www.travelweekly.com/Hotels/Tokyo/Hotel-Monterey-Hanzomon-p4355179
[12] Nest Hotel Tokyo Hanzomon - Hotels.com https://www.hotels.com/ho659471392/nest-hotel-tokyo-hanzomon-tokyo-japan/
[13] Nest Hotel Tokyo Hanzomon - Google https://www.google.com.kw/travel/hotels/entity/ChkIw8Xfl7vSm_QLGg0vZy8xMWhjdnc3bTM0EAE?ap=MABIAVqhAQoECDwQACIDS1dEKhYKBwjiDxAMGAsSBwjiDxAMGAwYASgAcgIIAooBVAoSCefITLEP3UFAER9HCzCNdmFAEhIJbaVvDz3eQUAR-UgeHsx2YUAaKgobEQzIFKesdmFAGSo3XmCm3UFACaejfmZSZbFAGgYI5gIQkAQlmplRQZIBAiABmgEHEgVUb2t5b6IBEQoIL20vMDdkZmsSBVRva3lv&g2lb=4181926%2C4208993%2C4209588%2C4207631%2C4215556%2C4219394%2C4220469&hl=en&un=0&ictx=1&sa=X&tcfs=EisKCC9tLzA3ZGZrEgVUb2t5bxoYCgoyMDE4LTEyLTExEgoyMDE4LTEyLTEyGAJSAA&ts=CAESCAoCCAMKAggDGjUKFRIRCggvbS8wN2RmazoFVG9reW8aABIcEhQKBwjqDxAFGAkSBwjqDxAFGA0YBDICEAA4ASoJCgU6A0tXRBoA&ei=ImKZafKnKuTvlsYPirqE8Q8&rp=OAHCAhwiGg0AAGBBEhMIhIOs_LTciQMVgOFLAx2fGC-U&ei=3RCaabzLHprllsYP9oqC2QI&ei=hCWaabT6I5jplsYP9NnQ-Qc&ved=2ahUKEwi0zOm3xeuSAxWYtMUCHfQsNH8QyvcEegUIBBCtAQ
[14] Nest Hotel Tokyo Hanzomon from $54. Tokyo Hotel Deals & Reviews https://www.kayak.com/Tokyo-Hotels-Nest-Hotel-Tokyo-Hanzomon.3558058.ksp
[15] Nest Hotel Tokyo Hanzomon - Trip.com https://us.trip.com/hotels/tokyo-hotel-detail-13999582/nest-hotel-tokyo-hanzomon/


---

# Output

<scratchpad>
Task Analysis:
 * Core task: The prompt asks the LLM to act as a Tokyo research assistant to validate, enrich, and format data about specific locations, outputting the result in a strict JSON schema.
 * Techniques: Role assignment (research assistant), step-by-step sequential logic, conditional routing (in Tokyo vs. not in Tokyo), exact formatting constraints (JSON only), and data grounding (providing the exact hotel coordinates).
 * Strengths: - Exceptionally well-structured. It anticipates edge cases (missing websites, locations outside Tokyo, missing coordinates) and provides explicit instructions for handling them.
   * The JSON schema is perfectly defined, down to the fallback strings.
   * Providing the base coordinates for the Nest Hotel is a great way to anchor the model and reduce hallucination.
 * Weaknesses & Blindspots:
   * The Math Problem: LLMs struggle with complex math, specifically the Haversine formula required to calculate straight-line distances between two coordinate points. The model is highly likely to hallucinate or approximate the distance inaccurately.
   * Strict JSON vs. Chain of Thought: By demanding the output only be the final JSON array, the user deprives the LLM of a "scratchpad" to think through the coordinates and distance calculation.
   * Sentence/Word counts: "Max 12 words" or "2-3 sentences" can sometimes be loosely interpreted by LLMs, though modern models are getting better.
 * Audio-Friendly Translation: Use conversational transitions ("Let's dive in", "Here's the catch"). Explain the "Haversine" issue simply as "LLMs are wordsmiths, not calculators."
   </scratchpad>
<Subject>
Prompt Breakdown: The Architect's Approach to Tokyo Data Extraction
</Subject>
<Message>
Hello there! Let's dive right into this prompt.
Right off the bat, I have to say—reading through your instructions felt like looking at a beautifully drawn architectural blueprint. You aren't just asking an AI for a favor; you're programming it. You've built a highly structured data-extraction pipeline, and it's clear you've thought deeply about how to corral an LLM into giving you exactly what you need.
Let's break down what's working really well here, because you've nailed several prompt engineering best practices.
First, your use of conditional logic is fantastic. You didn't just ask the model to pull data about a place; you added a gatekeeper step. By saying, "If it does not appear to be in Tokyo, set in_tokyo: false and fill the other fields with null," you are actively preventing the AI from hallucinating details to please you. You've given it a graceful way to fail if the input is bad.
Second, your JSON schema is airtight. You haven't left anything to the imagination. You specified exactly what the keys should be named, what data types to use, and exactly what fallback strings to insert if a piece of data is missing, like "No official website found." This level of constraint is exactly what you need if you plan to plug this output directly into a database or an app.
But, as with any blueprint, there's always a structural quirk we need to look out for. And in your prompt, that quirk is hiding in Step 4: the distance calculation.
Here's the catch: Large Language Models are brilliant wordsmiths, but they are notoriously clumsy calculators. To find the straight-line distance between your hotel and, say, the Tokyo Skytree, the model has to retrieve the Skytree's coordinates, hold them in its working memory, and then implicitly apply the Haversine formula—a complex bit of spherical trigonometry—to get the distance in kilometers. Because LLMs predict the next most likely token rather than crunching numbers like a traditional computer, there is a very high risk that it will confidently hallucinate that final distance.
Furthermore, you've commanded the model to return its final answer only as a JSON array, with no extra text. In prompt engineering, we call this a "zero-shot strict output." By forbidding the AI from outputting any extra text, you are denying it the ability to "think out loud." Cognitive science and AI research show us that LLMs perform significantly better on complex reasoning or math tasks when they are allowed to generate a "Chain of Thought"—essentially, showing their work before giving the final answer.
So, how do we fix this and elevate your prompt from great to bulletproof? I have a couple of suggestions for you to consider.
First, if you want the LLM to do the math, give it room to think. You could modify your prompt to ask the model to output a preliminary "thought process" block before generating the JSON. Or, even better, if you are using an API that supports a "JSON schema" or "Structured Output" mode, you can let the model output its reasoning into a specific calculation_scratchpad key right inside the JSON object itself.
However, if you are building this into an automated workflow, my strongest recommendation would be to decouple the math from the language model entirely. Let the LLM do what it does best: gather the coordinates, write that catchy 12-word headline, and format the JSON. Then, use a simple script—like a few lines of Python or JavaScript—to calculate the exact distance using those coordinates after the JSON is generated. It's always best to use the right tool for the job.
You also mentioned at the end that you might want to add an option for step-by-step transit directions. This is a wonderful idea for user experience, but keep in mind that transit routes are highly dynamic. They change based on the time of day, track maintenance, and train schedules. An LLM's knowledge is a static snapshot, so while it can give you a generally accurate route, it won't be real-time. Just something to keep in mind depending on how you plan to use this data!
Looking at the big picture, your prompt is robust, thoughtful, and incredibly well-structured. It really is a masterclass in setting constraints.
Would you like me to rewrite a version of your prompt that incorporates a "Chain of Thought" scratchpad so you can see how that might look in practice?
</Message>