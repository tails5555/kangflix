---
layout: page
title: Contact
description: Let's talk.
permalink: /contact/
---

<style type="text/css" media="screen">
  .container {
    margin: 0px auto;
    max-width: 600px;
  }
</style>

<div class="container">

  <h2>Contact With E-Mail</h2>
  <p>블로그 운영자의 메일로 전송되오니, <b>꼭 필요할 때 사용 바랍니다.</b></p>
  <div id="form" class="contact-form">
    <form accept-charset="UTF-8" method="POST" action="https://formspree.io/{{ site.email }}" v-on:submit.prevent="validateBeforeSubmit" ref="contact">
      <fieldset>
        <input type="hidden" name="_next" value="{{ site.url }}{{ site.baseurl }}/contact/message-sent/" />
        <input type="hidden" name="_language" value="ko" />

        <input type="text" name="name" placeholder="작성자" v-validate="'required'"
               :class="{ 'has-error': errors.has('name') }">
        <span v-if="errors.has('name')" v-cloak>${ errors.first('name') }</span>

        <input type="text" name="email" placeholder="작성자 E-Mail" v-validate="'required|email'"
               :class="{ 'has-error': errors.has('email') }">
        <span v-if="errors.has('email')" v-cloak>${ errors.first('email') }</span>

        <input type="text" name="_subject" placeholder="제목 입력" v-validate="'required'"
               :class="{ 'has-error': errors.has('_subject') }" />
        <span v-if="errors.has('_subject')" v-cloak>${ errors.first('_subject') }</span>

        <textarea name="message" onkeyup="adjust_textarea(this)" placeholder="내용 입력" v-validate="'required'"
                  :class="{ 'has-error': errors.has('message') }"></textarea>
        <span v-if="errors.has('message')" v-cloak>${ errors.first('message') }</span>

        <button type="submit">Send</button>
      </fieldset>
    </form>
  </div>

</div>

<script type="text/javascript">
function adjust_textarea(h) {
    h.style.height = "200px";
    h.style.height = (h.scrollHeight)+"px";
}
</script>

<script src="https://unpkg.com/vue@2.4.2"></script>
<script src="https://unpkg.com/vee-validate@2.0.0-rc.8"></script>
<script type="text/javascript">
Vue.use(VeeValidate);

new Vue({
  el: '#form',
  delimiters: ['${', '}'],
  methods: {
    validateBeforeSubmit: function () {
      this.$validator.validateAll();
      if (!this.errors.any()) {
        this.$refs.contact.submit();
      }
    }
  }
});
</script>
