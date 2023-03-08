Init commit

## UPDATE NEWS

1. Create `initState` with name: **newsUpdate**
2. Create function in reducer to set news update: **setNewsUpdate()**
3. In component `News` use `useEffect` to change initValues with dependecy `newuUpdate` from store `news` => set value from `priority` because response id (`number`)

1. 
```ts
const newUpdate = {
   "teamIds": number[],
      "id": number,
      "title": "string",
      "sapo": "string,
      "description": "string",
      "entityTypeId": 1,
      "status": number (1000 - 6000),
      "priority": number (1 - 3),
      "thumbnailImage": "stirng",
      "mainCategory": "News",
      "subCategory": "Nhân viên mới",
}
```

2. 

```ts
const handleConvertValuePriority(value: number){
    const priority = {
        1: PriorityValues.IMPORTANT,
        2: PriorityValues.HIGH,
        3: PriorityValues.LOW
    }
    
    return priority[value as keyof priority]
}

setNewsUpdate: (state: INewsStores, action: PayloadAction<INewsUpdate>) => {
    const newPriority = handleConvertValuePriority()
    const newNewsUpdate = {...values, priority: newPriority}
    state.newsUpdate = newNewsUpdate
}
```

3.

```ts
useEffect(() => {
    setInitValues(pNewsUpdate)
}, [pNewsUpdate])
```