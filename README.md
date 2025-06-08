import React, { useState } from 'react';
import { Light as SyntaxHighlighter } from 'react-syntax-highlighter';
import { docco } from 'react-syntax-highlighter/dist/esm/styles/hljs';

const CodeSnippetApp = () => {
  const [snippets, setSnippets] = useState([]);
  const [newSnippet, setNewSnippet] = useState('');
  const [language, setLanguage] = useState('javascript');

  const addSnippet = () => {
    if (newSnippet.trim() === '') return;
    setSnippets([...snippets, { code: newSnippet, language }]);
    setNewSnippet('');
  };

  return (
    <div className="p-4">
      <h1 className="text-2xl font-bold mb-4">Code Snippet Organizer</h1>
      <textarea
        className="w-full p-2 border rounded mb-2"
        rows="4"
        value={newSnippet}
        onChange={(e) => setNewSnippet(e.target.value)}
        placeholder="Enter your code snippet here..."
      ></textarea>
      <select
        className="mb-4 p-2 border rounded"
        value={language}
        onChange={(e) => setLanguage(e.target.value)}
      >
        <option value="javascript">JavaScript</option>
        <option value="python">Python</option>
        <option value="html">HTML</option>
        <option value="css">CSS</option>
      </select>
      <button
        className="bg-blue-500 text-white px-4 py-2 rounded"
        onClick={addSnippet}
      >
        Add Snippet
      </button>

      <div className="mt-4">
        {snippets.map((snippet, index) => (
          <div key={index} className="mb-4">
            <h2 className="text-lg font-semibold mb-2">Snippet {index + 1}</h2>
            <SyntaxHighlighter language={snippet.language} style={docco}>
              {snippet.code}
            </SyntaxHighlighter>
          </div>
        ))}
      </div>
    </div>
  );
};
