```
firebase login:list
firebase projects:list
```


---
## phamminhdao.com deployment

firebase.json

```
{
	"hosting": {
		"public": "public",
		"site": "pham-minh-dao",
		"ignore": ["firebase.json", "**/.*", "**/node_modules/**"]
	}
}
```

```
firebase deploy --only hosting:pham-minh-dao
```