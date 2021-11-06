### Component Hirarchy: ###

1. App (Functional component):

- Contains video fetching logic


2. SearchBar (class component)
3. VideoList child- VideoItem (Functional component)
4. VideoDetail (Functional component)


## Reusing logic Written Inside App component ##

- As the app.js is containing the video fetching logic, if we make any Analytics component, which will track the user's video searches, we can extract the logic into a custom hook and re-use it.

- Always remember, we need to re-use the logic only, we create custom hook. If we need to re-use JSX also, we create another component/ HOC.


# Custom Hooks #

- The best way to create resuable code in a react project (besides component!)
- Created by extracting hook-related code out of a function component.
- Custom hooks always make use of at-least one primitive hook internally.
- Each custom hook should have one purpose.
- Kind of an art form!
- Data-fetching is a great thing to try to make reusable.

## Process for Creating Reusable Hooks ##

- Identify each line of code related to some single purpose.
- Identify the inputs to that code.
- Identify outputs to that code.
- Extract all of the code into a separate function, receiving the inputs as arguments, and returning the outputs.  

```javaScript

import React , {useState, useEffect} from 'react';
import youtube from '../apis/youtube';

const useVideos = (defaultSearchTerm) => {
    const [videos, setVideos] = useState([]);

    useEffect( () => {
        search(defaultSearchTerm);
      }, [defaultSearchTerm]);
    
  const search = async (term) => {
    const response = await youtube.get("/search", {
      params: {
        q: term,
      },
    });

    setVideos(response.data.items)
  };

  return [videos, search]

};

export default useVideos;

// consume it in app.js : 
  const [videos, search] = useVideos('buildings');

  useEffect(() => {
      setSelectedVideo(videos[0])
  }, [videos]);

// JSX
  <VideoList
    onVideoSelect={onVideoSelect}
    videos={videos}
    />

```

# Redux #

1. Action Creator
2. Action
3. Dispatch
4. Reducers &larr; State/store











