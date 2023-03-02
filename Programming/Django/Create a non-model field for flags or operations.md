The gist of this is to add a field to your `serializer` and remove it in your `model.__init__()`. Then, in your `view`, handle the case where you need it. This way you can get the benefit of having it documented by doc generators.

```python
class MySerializer(ModelSerializer):
    my_write_only_data = CharField(allow_blank=True, required=False, write_only=True, help_text="Help text goes here for use with docs")
    
class MyModel(models.Model):
    def __init__(self, *args, **kwargs):
        if 'my_write_only_data' in kwargs:
          # or del kwargs['my_write_only_data']
          kwargs.pop('my_write_only_data')	
```
