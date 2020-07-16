# custom-hook-in-reactjs
Creating your own hook in Reactjs!


#### How
create file containing code like this:
```ts
import { useEffect, useState } from "react";

export const useDarkMode = () => {
  const [theme, setTheme] = useState<string>("light");

  const setMode = (mode): void => {
    typeof window !== "undefined"
      ? window.localStorage.setItem("theme", mode)
      : "";
    setTheme(mode);
  };

  const themeToggler = (): void => {
    theme === "light" ? setMode("dark") : setMode("light");
  };

  useEffect(() => {
    const localTheme = window.localStorage.getItem("theme");
    localTheme && setTheme(localTheme);
  }, []);
  return [theme, themeToggler];
};


```

#### Usage

import the file and use hook:

```ts
import  {useDarkMode} from "./components/useDarkMode"

const App = () => {
  const [theme, themeToggler] = useDarkMode();

  const themeMode = theme === "light" ? lightTheme : darkTheme;

  return (
    <ThemeProvider theme={themeMode}>
      <>
        <GlobalStyles />
        <div className="App">
          <Toggle theme={theme} toggleTheme={themeToggler} />
        </div>
      </>
    </ThemeProvider>
  );
};
export default App;
```
