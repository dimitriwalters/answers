# answers

Answers to interview-like questions

Q: How to refactor this code? [(source)](https://github.com/arialdomartini/Back-End-Developer-Interview-Questions)

```js
function()
{
  HRESULT error = S_OK;

  if(SUCCEEDED(Operation1()))
  {
    if(SUCCEEDED(Operation2()))
    {
      if(SUCCEEDED(Operation3()))
      {
        if(SUCCEEDED(Operation4()))
        {
        }
        else
        {
          error = OPERATION4FAILED;
        }
      }
      else
      {
        error = OPERATION3FAILED;
      }
    }
    else
    {
      error = OPERATION2FAILED;
    }
  }
  else
  {
    error = OPERATION1FAILED;
  }

  return error;
}
```

A: Like this

```js
function()
{
  if(!SUCCEEDED(Operation1())) return OPERATION1FAILED;
  if(!SUCCEEDED(Operation2())) return OPERATION2FAILED;
  if(!SUCCEEDED(Operation3())) return OPERATION3FAILED;
  if(!SUCCEEDED(Operation4())) return OPERATION4FAILED;
  return S_OK;
}
```

Q: Can you spot the memory leak? [(source)](https://github.com/arialdomartini/Back-End-Developer-Interview-Questions)

```js
public class Stack {
  private Object[] elements;
  private int size = 0;
  private static final int DEFAULT_INITIAL_CAPACITY = 16;

  public Stack() {
    elements = new Object[DEFAULT_INITIAL_CAPACITY];
  }

  public void push(Object e) {
    ensureCapacity();
    elements[size++] = e;
  }

  public Object pop() {
    if (size == 0)
      throw new EmptyStackException();
    return elements[--size];
  }

  /**
    * Ensure space for at least one more element, roughly
   *doubling the capacity each time the array needs to grow.
  */
  private void ensureCapacity() {
    if (elements.length == size)
      elements = Arrays.copyOf(elements, 2 * size + 1);
  }
}
```

A: `ensureCapacity` is not updating `size`
