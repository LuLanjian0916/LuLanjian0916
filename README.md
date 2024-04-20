<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>文章发布管理系统</title>
    <style>
        .container {
            width: 80%;
            margin: auto;
        }
        .form-group {
            margin-bottom: 10px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
        }
        .form-group input, .form-group textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .form-group button {
            padding: 8px 16px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .form-group button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
<div id="app" class="container">
    <h1>文章发布管理系统</h1>
    <div class="form-group">
        <label for="title">标题:</label>
        <input type="text" id="title" v-model="article.title" placeholder="请输入文章标题">
    </div>
    <div class="form-group">
        <label for="content">内容:</label>
        <textarea id="content" v-model="article.content" placeholder="请输入文章内容"></textarea>
    </div>
    <div class="form-group">
        <button @click="publishArticle">发布文章</button>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
    new Vue({
        el: '#app',
        data: {
            article: {
                title: '',
                content: ''
            }
        },
        methods: {
            publishArticle() {
                axios.post('/api/articles', this.article )
                    .then(response => {
                        alert('文章发布成功！');
                        // 清空表单
                        this.article.title = '';
                        this.article.content = '';
                    })
                    .catch(error => {
                        alert('文章发布失败！');
                    });
            }
        }
    });
</script>
</body>
</html>
