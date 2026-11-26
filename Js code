exports.handler = async (event) => {
  const { prompt } = JSON.parse(event.body);
  const apiKey = process.env.GEMINI_API_KEY;

  const fullPrompt = `You are FRIDAY, an AI agent created by HK_STUDIES. Create a complete single-file HTML website/app for: ${prompt}. Return ONLY full HTML code with CSS and JS inside, no explanation, no markdown. Make it beautiful, modern, mobile friendly.`;

  const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ contents: [{ parts: [{ text: fullPrompt }] }] })
  });

  const data = await response.json();
  let code = data.candidates?.[0]?.content?.parts?.[0]?.text || 'Error';
  code = code.replace(/```html/g, '').replace(/```/g, '');

  return { statusCode: 200, body: JSON.stringify({ code }) };
};
