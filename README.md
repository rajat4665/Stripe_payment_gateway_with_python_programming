# Stripe-payment-gateway-with-python-programming
In this repository, I am gonna show you how to play with stripe payment gateway, create customer , one-time payment and subscriprion

<h3></h3>
<h3>How to run this code:</h3>
<ul>
	<li>download this code from my GitHub</li>
	<li>open it into Jupyter notebook</li>
	<li>Now run its cells one by one</li>
</ul>
<h3>How to install jupyter notebook in Ubuntu:</h3>
open your terminal and paste these commands one by one.
<pre class="code-pre command"><code>sudo apt install python3-pip python3-dev</code></pre>
<pre class="code-pre command"><code>pip install jupyter</code></pre>
<h3>How to install jupyter notebook in windows:</h3>
Follow this <a href="https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/install.html">Link for windows</a>
<h3>Introduction:</h3>
Do you guys ever wonder how payment process work in E-commerce websites? The whole process work using API provided by a payment gateway provider and these provider charges some percent in the return, for example, stripe charge about 3 percent from a successful transition. One just needs to follow their procedure on how to integrate with your website. It is very easy because most of the payment gateway provides have really good documentation. There are lots of payment gateways are available in markets such as Paypal, Paytm, Wepay and Stripe.  I think you guys already heard about some of them.  In this post, I am gonna show you how one can set up stripe payment on their website. and how to set up a one-time payment, create customer and set subscription using stripe API.
<h3>Install these requirements:</h3>
<pre><span id="pip-command">pip install stripe</span></pre>
<h3>Setting up a Stripe Account :</h3>
<div id="setting-up-a-stripe-account">

Sign up for Stripe at <a href="https://dashboard.stripe.com/register" rel="nofollow">https://dashboard.stripe.com/register</a>.

</div>
<div id="using-the-stripe-api"></div>
<div>Read its official document for python from this <a href="https://stripe.com/docs/api/python" target="_blank" rel="noopener">link</a></div>
<div></div>
<div>Now go to api keys option under Developer section or simply follow this <a href="https://dashboard.stripe.com/test/apikeys">link</a></div>
<div></div>
<div></div>
<h3>Basic understanding of api:</h3>
There are two api keys one is live and other is test. For live one should attach their credit details. Test keys are available for everyone because it is just for testing and I am also demonstrate with test keys.

Now copy your Secret key  it is like <em><strong>"sk_test_********************* "</strong></em>
<h3><img class="alignnone size-full wp-image-111" src="https://getpython.files.wordpress.com/2019/06/screenshot-from-2019-06-30-23-32-14.png" alt="Screenshot from 2019-06-30 23-32-14" width="1037" height="193" /></h3>
 
<h3>Lets start playing with this api:</h3>
First of all import stripe module and place your test api key in a variable
<pre>import stripe
stripe.api_key = "sk_testxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"</pre>
<strong>Create Customer</strong>

Now create customer because we need customer to process any payment in stripe
<pre>stripe.Customer.create(
  description="Customer for rajat4665@gmail.com",
    name = 'Rajat',
    email = "rajat4665@gmail.com",
)
# it return a json respone where you can store its customer id for further process
#<Customer customer id=cus_FLpFgWascPQNba at 0x7ff8c8189188> JSON:{}</pre>
Go to this <a href="https://dashboard.stripe.com/test/customers">link</a> and see customer is register successfully

<img class="alignnone size-full wp-image-114" src="https://getpython.files.wordpress.com/2019/06/screenshot-from-2019-07-01-00-16-37.png" alt="Screenshot from 2019-07-01 00-16-37" width="1076" height="347" />

 
<h3>How to fetch data of existing customers:</h3>
customer_data = stripe.Customer.retrieve('Customer_id')

 
<h3>One-time payment:</h3>
One-time payment is known as charge in the world of stripe payments. So we need to create charge.
<pre>stripe.Charge.create(
  amount=2000, # amount is $20 it show 20*100
  currency="usd", # currency
  source="tok_mastercard", # this is default
  description="Charge for jenny.rajat4665@example.com"
)

"""
it return charge id , txt id in return store it in your database</pre>
<pre><Charge charge id=ch_1Er87vIypo2lmEr6BNf5X2bt at 0x7ff8c80c7e08> JSON: {
  "amount": 2000,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_1Er87vIypo2lmEr61eixqsP0",\
"""</pre>
<pre></pre>
<img class="alignnone size-full wp-image-115" src="https://getpython.files.wordpress.com/2019/06/screenshot-from-2019-07-01-00-23-44.png" alt="Screenshot from 2019-07-01 00-23-44.png" width="1069" height="425" />

As you can see , one time payment has been done.

 
<h3>How to create Subscriprion in stripe :</h3>
First of all we need plans which user can subscribe , so go to <a href="https://dashboard.stripe.com/test/subscriptions/products">link</a> of stripe and create a plan.

<img class="alignnone size-full wp-image-116" src="https://getpython.files.wordpress.com/2019/06/screenshot-from-2019-07-01-00-29-04.png" alt="Screenshot from 2019-07-01 00-29-04" width="1068" height="365" />

Now click on new for create  a product plan  by click on new button and fill basic details like name , currency, price and <span style="color: var(--color-text);">Billing interval</span>

<img class="alignnone size-full wp-image-117" src="https://getpython.files.wordpress.com/2019/06/screenshot-from-2019-07-01-00-53-04.png" alt="Screenshot from 2019-07-01 00-53-04.png" width="1060" height="362" />

As you can see i have created one plan.

fetch existing plan , bellow code will display all existing plans from you api , Here you need to capture plan_id it will use in subscription proceess
<pre>plan = stripe.Plan.list()
plan_id = plan['data'][0]['id']</pre>
 

Now we have created plan , created customer and we have plan id . Now time to create subscription
<pre># create Subscription
stripe.Subscription.create(
  customer="cus_F2W1hNSAYf7pUm",# this is customer id who want to buy this subscription
  items=[
    {
      "plan": "plan_F2VGZl0q6F51Cf", # this plan id of particular plan
    },
  ]
)

# it will also return json response save it and mark subscription id
# subscription_id will use to cancel, update and track payment.

</pre>
You can see its payment in transaction section.

<img class="alignnone size-full wp-image-118" src="https://getpython.files.wordpress.com/2019/06/screenshot-from-2019-07-01-01-04-17.png" alt="Screenshot from 2019-07-01 01-04-17" width="1013" height="403" />

And also check more details in subscription section.
<h3><img class="alignnone size-full wp-image-119" src="https://getpython.files.wordpress.com/2019/06/screenshot-from-2019-07-01-01-04-35.png" alt="Screenshot from 2019-07-01 01-04-35" width="1108" height="532" /></h3>
<h3>How to cancel this Subscription:</h3>
<pre> stripe.Subscription.delete('sub_id')</pre>
<strong>Moreover, you can also delete customer from stripe:</strong>
<div class="method-example-request include-prompt">
<div class="method-example-request-body">
<div class="CodeBlock">
<div class="CodeBlock-scroll">
<pre class="CodeBlock-pre language-python"><code class=" language-python">stripe<span class="token punctuation">.</span>Customer<span class="token punctuation">.</span>delete<span class="token punctuation">(</span><span class="token string">'cus_id'</span><span class="token punctuation">)</span></code></pre>
</div>
</div>
</div>
</div>
<div class="method-example-response">
<div class="method-example-response-title">Thank you for reading this article, stay tuned for more updates!!!!!!!</div>
</div>
<h2></h2>
<h2>References:</h2>
https://stripe.com/docs/api?lang=python
