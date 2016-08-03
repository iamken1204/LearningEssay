# The real workable JS libs choosed by Kettan

#### Datetime picker
* [CuriousSolutions/DateTimePicker](https://github.com/CuriousSolutions/DateTimePicker)
    * :white_check_mark: can run on browser
    * :white_check_mark: [jsdelivr](https://www.jsdelivr.com/projects/datetimepicker)
    * dependencies:
        1. jquery

#### AJAX
* [fdaciuk/ajax](https://github.com/fdaciuk/ajax)
      * :white_check_mark: can run on browser
      * :white_check_mark: CDN:
      ```html
      <script src="//cdn.rawgit.com/fdaciuk/ajax/v2.1.2/dist/ajax.min.js"></script>
      ```
      * :white_check_mark: vanilla js
      * :heavy_exclamation_mark: Can not use?   
      Try [my version](https://gist.github.com/iamken1204/60b534bcb2a3b0fca128776d4cb37f24)   
      Example:   
      
      ```javascript
      let request = AJAX.request({
        headers: {
          'X-CSRF-TOKEN': document.querySelector('#csrf-token').getAttribute('content')
        },
        method: 'post',
        url: '/admin/news/' + document.getElementById('id').value,
        data: data
      }).then(function (res) {
        if (res.code === 200) {
          confirm('編輯成功！')
          window.location.replace(document.getElementById('back').value)
        } else {
          alert('伺服器回應錯誤\n' + res.msg)
        }
      })
      ```
