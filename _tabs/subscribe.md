---
title: Subscribe
icon: fas fa-address-book 
order: 5
---
<script type="text/javascript">
function validation(){
var email = document.getElementById("mce-EMAIL").value;
if (ValidateEmail(email)){
	toggleHidden('subscribe-success');
	return true;
}
else 
return false;

}

function ValidateEmail(mail) 
{
if(typeof mail=== "undefined")
{
	alert('Please enter a valid email address');
	return false;
}
 if (/^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/.test(mail))
  {
    return (true);
  }
  else{
    alert("You have entered an invalid email address!");
    return false;
	}
}

function toggleHidden(id){
  var attr = document.getElementById(id);
  if (attr.style.display == "none") 
	 attr.style.display = "block";
   else 
    attr.style.display = "none";
  }
</script>
<div id="mc_embed_signup">
		<div> 
		Do you want to be notified when a new blog is published at devtechblogs.com? If yes,  please sign up with your email?
		</div>
		<div>
		You can unsubscribe from the mailing list at any time if you wish to do so.
		</div>
		<div class="form-group">
			<div>
            <h3>SIGN UP</h3>
			</div>
            <form action="https://gmail.us6.list-manage.com/subscribe/post?u=0e25126063c9c97a48d665d46&amp;id=a797462a9d" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form"  target="_blank" novalidate>
			 
			<div class="form-group" id="mc_embed_signup_scroll">
				<label for="mce-EMAIL"><i class="fas fa-envelope fa-lg me-3 fa-fw"></i> Email address</label>
				<input type="email" value="" name="EMAIL" class="form-control col-lg-7" id="mce-EMAIL" aria-describedby="emailHelp" placeholder="Enter your Email">
				<small id="emailHelp" class="form-text text-danger">*Your email will be added to mailing list only and will never be shared with anyone else</small>
				<div id="subscribe-success" style="display:none;"><small class="form-text text-success" >*Congrats! You have subscribed to Dev Tech Blogs</small></div>
				<div style="position: absolute; left: -5000px;" aria-hidden="true"><input type="text" name="b_0e25126063c9c97a48d665d46_a797462a9d" tabindex="-1" value=""></div>
			</div>
			<div>
				<input type="submit" value="Subscribe" onclick="return validation()" name="subscribe" class="btn btn-primary" id="mc-embedded-subscribe">
			</div>
	
            </form>
		</div>
</div>
	
    
		
	