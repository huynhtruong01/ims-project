## Edit comment
- State `edit` to check comment have edit
- Comment will transform form includes `value of comment`
- Add button `Hủy` in Comment Actions

### Redux Edit Comment

- Send `commentRoot` and `id comment reply` (if have) 
- If `commentRoot === id comment`, edit id of commentRoot
- Otherwise `edit into comment have reply`, `findIndex` and edit it

```ts
editComment: (state: INewsStore, action: PayloadAction<any>) => {
    if(action.payload.comment.commentRoot === action.payload.idComment){
        const index = state.news.detailCommentList.findIndex((x) => x.id === action.payload.idComment)
        
        if(index >= 0){
            state.news.detailCommentList[index].comment = action.payload.comment.comment
            state.news.detailCommentList = [...state.news.detailCommentList]
        }
        
        return
    }
    
    const indexComment = state.news.detailCommentList.findIndex((x) => x.commentRoot === action.payload.comment.commentRoot)
    
    if(indexComment < 0) return
    
    const replyCommentList = state.news.detailCommentList[action.payload.comment.commentRoot]?.reply
    
    const index = replyCommentList.findIndex((x) => x.id === action.payload.idComment)
    if(index >= 0){
        replyCommentList[index].comment = action.payload.comment.comment
        replyCommentList = [...replyCommentList]
        state.news.detailCommentList[action.payload.comment.commentRoot]?.reply = [...replyCommentList]
        state.news.detailCommentList = [...state.news.detailCommentList]
    }
}
```

---

## Delete Comment

- When click `Xóa` show a component to delete?

### Redux delete

```ts
deleteComment: (state: INewsStore, payload: PayloadAction<any>) => {
    if(action.payload.comment.commentRoot === action.payload.idComment) {
        const index = state.news.detailCommentList.findIndex((x) => x.id === action.payload.idComment)
        
        if(index >= 0){
            const newDetailCommentList = state.news.detailCommentList.filter(x => x.id !== action.payload.idComment)
            
            state.news.detailCommentList = [...newDetailCommentList]
        }
        return
    }
    
    const commentById = state.news.detailCommentList.findIndex(x => x.commentRoot === action.payload.comment.commentRoot)
    
    if(commentById < 0) return
    const replyCommentList = commentById?.reply
    
    const index = replyCommentList.findIndex(x => x.id === action.payload.idComment)
    if(index >= 0){
        const newReplyCommentList = replyCommentList.filter(x => x.id !== action.payload.idComment)
        
        action.payload.detailCommentList[index].reply = newReplyCommentList
        action.payload.detailCommentList = [...action.payload.detailCommentList]
    }
}















```