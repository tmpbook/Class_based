"""========================================
###混合类AjaxableResponseMixin，为了让views同时支持ajax提交表单
==========================================="""
```python
class AjaxableResponseMixin(object):
    """
    Mixin to add AJAX support to a form.
    Must be used with an object-based FormView (e.g. CreateView)
    """
    def render_to_json_response(self, context, **response_kwargs):
        data = json.dumps(context)
        response_kwargs['content_type'] = 'application/json'
        return HttpResponse(data, **response_kwargs)
    
    def form_invalid(self, form):
        print "表单不合法"
        response = super(AjaxableResponseMixin, self).form_invalid(form)
        # 如果他是ajax请求且验证未通过
        if self.request.is_ajax():
            return self.render_to_json_response(form.error, status=400)
        # 如果他不是ajax请求而且它表单验证没通过
        else:
            return self.render_to_response(RequestContext(self.request, {'form': form}))
            #return HttpResponse("form is invalid.. this is just an HttpResponse object")

    def form_valid(self, form):
        # We make sure to call the parent's form_valid() method because
        # it might do some processing (in the case of CreateView, it will
        # call form.save() for example).
        print "表单合法"
        response = super(AjaxableResponseMixin, self).form_valid(form)
        if self.request.is_ajax():
            data = {
                    # 返回给前端的（json格式）
                    'pk': self.object.pk,
            }
            return self.render_to_json_response(data)
        else:
            return response
    
class AuthorCreate(AjaxableResponseMixin, CreateView):
    model = Author
    fields = ['name', 'salutation']
    
    # 重载dispatch使用装饰器（@csrf_exempt）为每个instence添加例外，不进行跨站攻击防护
    #@csrf_exempt
    def dispatch(self, *args, **kwargs):
        return super(AuthorCreate, self).dispatch(*args, **kwargs)
```
