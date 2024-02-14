---
layout: pages
title: "About"
permalink: /about/
author_profile: false
---

<p><div style="border:#aaa 1px solid;border-radius:50%;overflow:hidden;width:10%;height:auto;">
  <img src="/assets/images/portrait.jpg" width="100%" style="user-select:none;-webkit-user-drag:none;">
</div></p>

<div class = "div1" markdown="1">
  <p>👤 이성진</p>
  🏫 경희대학교<br>
  📝 전자공학과<br>
  🎓 4학년<br>
  💼 학생입니다.
</div>

<div class = "div2" markdown="1">
  <p>👤 LEE SUNGJIN</p>
  🏫 Kyunghee University<br>
  📝 Electronic Engineering<br>
  🎓 Senior<br>
  💼 Student.
</div>

#### 🌐&nbsp;Contact Me

<a href="https://github.com/asungajinli" class="contact" target="_blank" rel="me">
  <i class="fab fa-fw fa-github" aria-hidden="true"></i>
</a>
&nbsp;&nbsp;
<a href="https://instagram.com/sdin.99" class="contact" target="_blank" rel="me">
  <i class="fab fa-fw fa-instagram" aria-hidden="true"></i>
</a>
&nbsp;&nbsp;
<span class="contact modal-link" alt="" data-target="modalContainer" rel="me">
  <i class="fas fa-fw fa-comment" style="cursor:pointer;" aria-hidden="true"></i>
</span>
&nbsp;&nbsp;
<a href="https://www.linkedin.com/in/asungajinli" class="contact" target="_blank" rel="me">
  <i class="fab fa-fw fa-linkedin" aria-hidden="true"></i>
</a>
&nbsp;&nbsp;
<a href="mailto:ssjj3552@gmail.com" class="contact" style="margin-bottom:8rem;" rel="me">
  <i class="fas fa-fw fa-envelope-square" aria-hidden="true"></i>
</a>

#### <i class="fas fa-fw fa-copyright" aria-hidden="true"></i> Copyright
Copyright 2024. Lee Sung Jin All pictures cannot be copied without permission.<br>
<a href="/copyright/" style="text-decoration:none;" rel="nofollow noopener noreferrer"> Copyright Attribution</a>

---

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
  $('.modal-link').on('click', function() {
      $('#modalContainer').fadeIn();
      var imgSrc = '/assets/images/KakaoAddFriend.png';
      var imgAlt = 'QR코드를 찍으세요';
      $('#modalImage').attr('src', imgSrc);
      $('#caption').html(imgAlt);
      $('#modalContainer').css("display", "flex")
      initializeModal();
  });
  $('#modalImage').on('mouseenter', function(e) {
    $(this).css('cursor', 'grab');
  });
  $("#modalContent").draggable();
  $(document).mousedown(function(e) {
      if (!$('#modalContent').is(e.target) && $('#modalContent').has(e.target).length === 0) {
          $('#modalContainer').fadeOut();
          $('body').css("overflow-y", "scroll");
      }
  });
  $(document).keydown(function(e) {
    if (e.keyCode == 27) {
      $('#modalContainer').fadeOut();
      $('body').css("overflow-y", "scroll");
    }
  });
</script>