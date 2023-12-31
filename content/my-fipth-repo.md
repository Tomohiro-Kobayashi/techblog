+++
title = 'My Second Repo'
date = 2023-12-30T23:36:44+09:00
draft = false
description = "This is description"
image = "/images/5s.webp"
imageBig = "/images/5b.webp"
categories = ["general", "life", "music"]
authors = ["Tomohiro"]
avatar = "/images/icon.webp"
+++

# 見出し1


markdownサンプル文章です。ここは地の文です。

markdownでは、箇条書きは*や-などの記号を文頭に置くことで記述します。箇条書きの階層は行頭スペース4つを足します。

## 見出し2


markdownサンプル文章です。ここは地の文です。

markdownでは、箇条書きは*や-などの記号を文頭に置くことで記述します。箇条書きの階層は行頭スペース4つを足します。


# 見出し1


markdownサンプル文章です。ここは地の文です。

markdownでは、箇条書きは*や-などの記号を文頭に置くことで記述します。箇条書きの階層は行頭スペース4つを足します。

### 見出し3


markdownサンプル文章です。ここは地の文です。

markdownでは、箇条書きは*や-などの記号を文頭に置くことで記述します。箇条書きの階層は行頭スペース4つを足します。

#### 見出し4

markdownサンプル文章です。ここは地の文です。

markdownでは、箇条書きは*や-などの記号を文頭に置くことで記述します。箇条書きの階層は行頭スペース4つを足します。

- これはひとつめの箇条書き
- ふたつめの箇条書き
    - 一つ階層が深い箇条書き
- みっつめの箇条書き

### コード

3つのバッククォート記号でくくることで、コード例を示します

```
[ozuma@vpscon ~]$ cp a
cp: missing destination file operand after `a'
Try `cp --help' for more information.
```

```python
from fastapi import FastAPI
from fastapi.responses import JSONResponse
from fastapi.encoders import jsonable_encoder
from fastapi import HTTPException
from typing import List
from sqlalchemy.orm import Session
from . import models, schemas
from .database import SessionLocal, engine

models.Base.metadata.create_all(bind=engine)

app = FastAPI()

# Dependency
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

@app.post("/authors/", response_model=schemas.Author)
def create_author(author: schemas.AuthorCreate, db: Session = Depends(get_db)):
    db_author = models.Author(name=author.name)
    db.add(db_author)
    db.commit()
    db.refresh(db_author)
    return db_author

@app.get("/authors/", response_model=List[schemas.Author])
def read_authors(skip: int = 0, limit: int = 100, db: Session = Depends(get_db)):
    authors = db.query(models.Author).offset(skip).limit(limit).all()
    return authors

@app.get("/authors/{author_id}", response_model=schemas.Author)
def read_author(author_id: int, db: Session = Depends(get_db)):
    db_author = db.query(models.Author).filter(models.Author.id == author_id).first()
    if db_author is None:
        raise HTTPException(status_code=404, detail="Author not found")
    return db_author

@app.put("/authors/{author_id}", response_model=schemas.Author)
def update_author(author_id: int, author: schemas.AuthorCreate, db: Session = Depends(get_db)):
    db_author = db.query(models.Author).filter(models.Author.id == author_id).first()
    if db_author is None:
        raise HTTPException(status_code=404, detail="Author not found")
    db_author.name = author.name
    db.commit()
    db.refresh(db_author)
    return db_author

@app.delete("/authors/{author_id}", response_class=JSONResponse)
def delete_author(author_id: int, db: Session = Depends(get_db)):
    db_author = db.query(models.Author).filter(models.Author.id == author_id).first()
    if db_author is None:
        raise HTTPException(status_code=404, detail="Author not found")
    db.delete(db_author)
    db.commit()
    return JSONResponse(content=jsonable_encoder({"message": "Author deleted"}))
```

markdown形式については、Wikipediaなども参照ください
- http://ja.wikipedia.org/wiki/Markdown