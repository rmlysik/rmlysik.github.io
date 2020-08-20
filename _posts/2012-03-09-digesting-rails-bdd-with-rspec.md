---
title: 'Digesting Rails: BDD with RSpec'
date: '2012-03-09 00:19:26 -0500'
date_gmt: '2012-03-09 05:19:26 -0500'
categories:
- Ruby on Rails
- Ruby
- BDD
- RSpec
tags: []
comments:
- id: 91
  author: Vandeson
  author_email: s.prurouy@mail.com.au
  author_url: http://www.facebook.com/profile.php?id=100003405767972
  date: '2012-04-16 22:14:34 -0400'
  date_gmt: '2012-04-17 02:14:34 -0400'
  content: in his Google video, there are still a high percentage of eppole who practices
    bad TDD. But there is also eppole who is practicing BDD while their doing TDD.
    So what is the difference? The one thing I have seen is that most eppole think
    that TDD is about Testing. When you explain that TDD is really at its hart a design
    process, they squawk at you and give you a look like you&rsquo;ve lost your mind.I
    see TDD as performing the following roles:1. Design process2. Requirements Capturing3.
    Behavior Specification4. Regression Test SuiteFor this reason I think we need
    a Behavior-Driven Development framework.My daily development environment is .NET
    and C#, thus I would like to have something that suites my needs. Dave is working
    on rSpec for RoR and then there is JBehave for java. But I was unable to find
    anything for the .NET space. So I thought, I will roll my own.Here is what I have
    so far:using NBehave;namespace SampleBehaviour{    [ Functionality ]    public
    class CustomerLoadBehaviour    {        private Customer customer = null;        [InitializeSpecification()]        public
    void Setup()        {            customer = new Customer(123);        }        [
    Specification() ]        public void ShouldLoadCustomer()        {            Behaviour.Of(
    customer.Id ).Must.Not.Be.Null(  The Customer Id must not be null.  );            Behaviour.Of(
    customer.Id ).Must.Equal( 123,  The customer id's aren't equal  );        }        [
    Specification() ]        public void LoadCustomerShouldFailed()        {            Behaviour.Of(customer.Id).Must.Not.Be.Null(
    The Customer Id must not be null. );            Behaviour.Of( customer.Id ).Must.Not.Equal(
    125,  The customer id's aren't equal  );        }    }}I&rsquo;m busy working
    on a TestTip for VS2005, but have finished the NUnit integration.
---
I've now progressed through the first six chapters of the [Ruby on Rails Tutorial](https://www.railstutorial.org/book "Ruby on Rails Tutorial"){:target="_blank"} and my head is spinning. I feel like Keanu Reeve's character from the 90's b-movie [Johnny Mnemonic](https://www.imdb.com/title/tt0113481/ "Johnny Menmonic"){:target="_blank"}. Before I proceed, I thought I'd take some time to digest what I've learned and do a little research into aspects that I've found somewhat inscrutable, which are legion. Where to start? I'm somewhat intrigued by the idea of Test Driven Development, or in the case of the Ruby on Rails tutorial its variant which is described as Behavior Driven Development.

### Behavior Driven Development

Behavior Driven Development or BDD is a framework for unit testing of software that seeks to rephrase test cases using more natural language. Unit tests are described as examples of how the system should behave. BDD is not a radical re-invention of Test Driven Development, but rather an extension or re-interpretation of it. To understand more about how Behavior Driven Development came about, I recommend reading the article [Introducing BDD](http://dannorth.net/introducing-bdd/ "Introducing BDD"){:target="_blank"} by Dan North.

### RSpec

RSpec is a Behavior Driven Development tool for Ruby inspired by the work of Dan North and JBehave. This tool enables the execution of human readable test specifications and provides methods to generate readable test result documentation. To understand more about RSpec, I recommend the following articles:

*   [An Introduction to RSpec](http://blog.davidchelimsky.net/blog/2007/05/14/an-introduction-to-rspec-part-i/ "An Introduction to RSpec"){:target="_blank"} by David Chelimsky.
*   [RSpec Best Practices](http://www.methodsandtools.com/tools/tools.php?rspec "RSpec Best Practices"){:target="_blank"} by Jared Carroll.
*   [Ruby for Newbies: Testing with RSpec](https://code.tutsplus.com/tutorials/ruby-for-newbies-testing-with-rspec--net-21297 "Ruby for Newbies: Testing with RSpec"){:target="_blank"} by Andrew Burgess.
*   [Ruby on Rails Tutorial](https://www.railstutorial.org/book/static_pages#sec-getting_started_with_testing "Ruby on Rails Tutorial"){:target="_blank"} by Michael Hartl.

### A Simple Example

The Ruby on Rails Tutorial contains an excellent overview of BDD and RSpec and interweaves testing using RSpec throughout each chapter. Rails is set up out of the box to incorporate a unit testing framework like RSpec.

It is possible to use RSpec without the Rails framework, however. This simplifies things considerably but still allows for a useful demonstration of what RSpec is all about. 

Please note that the examples that follow are geared for the Mac OS X environment. I'm assuming you've already installed Ruby and Gem. You'll also need to have RSpec installed, so open a command shell and type the following command:

{% highlight shell %}
$ gem install rspec
{% endhighlight %}

You should get a response like the following:

{% highlight shell %}
Successfully installed rspec-2.8.0
1 gem installed
Installing ri documentation for rspec-2.8.0...
Installing RDoc documentation for rspec-2.8.0...
{% endhighlight %}

You may want to create a directory where for our test files at this point:

{% highlight shell %}
mkdir rspec_example
cd rspec_example
{% endhighlight %}

When doing test driven development the typical workflow is a follows:

*    Write a test that describes the behavior of a part of the system.
*    Run the test ensuring that it fails because the code has not yet been written.
*    Write just enough code to make the test pass.
*    Run the test to confirm that the test now passes.

If necessary, the code can then be refactored without changing its function. The validity of the refactored code can then be confirmed by running the test again.

I'll use a BankAccount class to demonstrate the concept behind test driven development. The BankAccount class keeps track of someone's bank balance and provides methods to handle deposits and withdrawals.

Let's start by creating the test specification for our (yet to be developed) BankAccount class. Open your favorite text editor and save the following as bankaccount_spec.rb:

{% highlight ruby %}
require './bankaccount'

describe BankAccount do
end
{% endhighlight %}

Note the "./" preceding the file name for the BankAccount class. This is necessary when referring to a file within the same directory. 

The `describe` method creates an `ExampleGroup` for the BankAccount class. At this point we haven't created any examples yet, but our class behavior examples will later be defined within this block. 

Let's run RSpec to confirm that the test fails as expected. At the shell prompt enter the command to run RSpec for our bankaccount_spec.rb:

{% highlight shell %}
$ rspec bankaccount_spec.rb
cannot load such file -- ./bankaccount (LoadError)
{% endhighlight %}

The test failed as expected since the file doesn't exist yet. Let's remedy this by creating the BankAccount.rb file:

{% highlight ruby %}
class BankAccount
end
{% endhighlight %}

Not very interesting yet, but our test should pass this time. From the shell prompt run the rspec command again:

{% highlight shell %}
$ rspec bankaccount_spec.rb
No examples found.

Finished in 0.00004 seconds
0 examples, 0 failures
{% endhighlight %}

Our spec contained no examples, so the result "0 examples, 0 failures" is the expected result. Whew...

When a new BankAccount instance is created, it should start with a zero balance. Let's create our first example to validate this behavior:

Edit the bankaccount_spec.rb file to add the following statements:

{% highlight ruby %}
require './bankaccount'

describe BankAccount do

  it "sets initial balance to zero" do
    @account = BankAccount.new
    @account.balance.should eq(0.00)
  end

end
{% endhighlight %}

So, what's up with "it?" `it` turns out to be a method that returns an instance of an `Example`. `it` takes two parameters, a name, and a block that contains our test. In this test, we're creating an instance of BankAccount and then verifying that the balance is equal to zero. 

Now, when we run RSpec again, we *should* get an error, since the `balance` method has not yet been defined in our BankAccount class.

NOTE: You can use the `--format documentation` option with `rspec` to display example names in the output.

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  sets initial balance to zero (FAILED - 1)

Failures:

  1) BankAccount sets initial balance to zero
     Failure/Error: @account.balance.should eq(0.00)
     NoMethodError:
       undefined method `balance' for #<BankAccount:0x007f92db1f4850>
     # ./bankaccount_spec.rb:7:in `block (2 levels) in <top (required)>'

Finished in 0.00055 seconds
1 example, 1 failure

Failed examples:

rspec ./bankaccount_spec.rb:5 # BankAccount sets initial balance to zero
{% endhighlight %}

Now we'll add the code to our BankAccount.rb file to get this test to pass:

{% highlight ruby %}
class BankAccount
  def initialize
    @balance = 0.00
  end

  def balance
    @balance
  end
end
{% endhighlight %}

The `initialize` constructor for our BankAccount class sets the balance to zero. We've also defined the `balance` getter method for our balance property. When we run the test again it should pass:

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  sets initial balance to zero

Finished in 0.0006 seconds
1 example, 0 failures
{% endhighlight %}

Voila! Let's next add an example to our spec for the `deposit` method. Each example describes an expected behavior of the system under test. The expected behavior of the `deposit` method is that the balance will have increased by the amount of the deposit.

Edit the bankaccount_spec.rb file to add the deposit example:

{% highlight ruby %}
require './bankaccount'

describe BankAccount do

  it "sets initial balance to zero" do
    @account = BankAccount.new
    @account.balance.should eq(0.00)
  end

  it "increases balance by amount of deposit" do
    @account = BankAccount.new
    @account.deposit 100.00
    @account.balance.should eq(100.00)
  end

end
{% endhighlight %}

In this test, we're creating an instance of BankAccount and calling its `deposit` method with a value of 100.00. The expected behavior of this method call is that the balance for the account has increased by 100.00. We're validating the result using the `should` method which takes `eq(100)` as a parameter.

Now, when we run RSpec again, we *should* get an error, since the `deposit` method has not yet been defined in our BankAccount class.

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  sets initial balance to zero
  increases balance by amount of deposit (FAILED - 1)

Failures:

  1) BankAccount increases balance by amount of deposit
     Failure/Error: @account.deposit 100.00
     NoMethodError:
       undefined method `deposit' for #<BankAccount:0x007fa3aa350688 @balance=0.0>
     # ./bankaccount_spec.rb:12:in `block (2 levels) in <top (required)>'

Finished in 0.00187 seconds
2 examples, 1 failure

Failed examples:

rspec ./bankaccount_spec.rb:10 # BankAccount increases balance by amount of deposit
{% endhighlight %}

Now let's try to get this test to pass by defining the `deposit` method. Edit the BankAccount.rb file to include the `deposit` method:

{% highlight ruby %}
class BankAccount

  def initialize
    @balance = 0.00
  end

  def balance
    @balance
  end

  def deposit (amount)
    @balance += amount
  end

end
{% endhighlight %}

Now when we run RSpec again, the test should pass:

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  sets initial balance to zero
  increases balance by amount of deposit

Finished in 0.00063 seconds
2 examples, 0 failures
{% endhighlight %}

Wow...that actually worked! 

At this point let's take a moment to refactor some of the code in our spec. RSpec allows you to define a `before` block where you can perform setup tasks. You may have noticed that in each of the examples in our test we are creating an instance of BankAccount. Let's put that in a `before` block at the top of our bankaccount_spec:

{% highlight ruby %}
require './bankaccount'

describe BankAccount do

  before :each do
    @account = BankAccount.new
  end

  it "sets initial balance to zero" do
    @account.balance.should eq(0.00)
  end

  it "increases balance by amount of deposit" do
    @account.deposit 100.00
    @account.balance.should eq(100.00)
  end

end
{% endhighlight %}

The `:each` symbol indicates that this setup block should be executed before each test.

Let's run rspec again to be sure that this didn't break anything:

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  sets initial balance to zero
  increases balance by amount of deposit

Finished in 0.00065 seconds
2 examples, 0 failures
{% endhighlight %}

Looking good! Buoyed by this success, let's add an example for the as yet to be defined `withdraw` method to the bankaccount_spec.rb file:

{% highlight ruby %}
require './bankaccount'

describe BankAccount do

  before :each do
    @account = BankAccount.new
  end

  it "sets initial balance to zero" do
    @account.balance.should eq(0.00)
  end

  it "increases balance by amount of deposit" do
    @account.deposit 100.00
    @account.balance.should eq(100.00)
  end

  it "decreases balance by amount of withdrawal" do
    @account.deposit 100.00
    @account.withdraw 10.00
    @account.balance.should eq(90.00)
  end
end
{% endhighlight %}

The expected behavior of the withdraw method is that the balance should be decreased by the amount of the withdrawal. Let's run the test again to confirm that it fails:

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  sets initial balance to zero
  increases balance by amount of deposit
  decreases balance by amount of withdrawal (FAILED - 1)

Failures:

  1) BankAccount decreases balance by amount of withdrawal
     Failure/Error: @account.withdraw 10.00
     NoMethodError:
       undefined method `withdraw' for #<BankAccount:0x007fe459201df0 @balance=100.0>
     # ./bankaccount_spec.rb:20:in `block (2 levels) in <top (required)>'

Finished in 0.00101 seconds
3 examples, 1 failure

Failed examples:

rspec ./bankaccount_spec.rb:18 # BankAccount decreases balance by amount of withdrawal
{% endhighlight %}

Now we'll write code to get this test to pass:

{% highlight ruby %}
class BankAccount
  def initialize
    @balance = 0.00
  end

  def balance
    @balance
  end

  def deposit (amount)
    @balance += amount
  end

  def withdraw (amount)
    @balance -= amount
  end
end
{% endhighlight %}

Now when we run the test again it should pass:

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  sets initial balance to zero
  increases balance by amount of deposit
  decreases balance by amount of withdrawal

Finished in 0.00142 seconds
3 examples, 0 failures
{% endhighlight %}

OK, (brushing hands together) it looks like we're done. But wait, what if there are insufficient funds to cover the withdrawal amount? We should add an example for that also. 

Before we do, let's refactor the test code to incorporate some of the recommendations from Jared Caroll's article [RSpec Best Practices](http://www.methodsandtools.com/tools/tools.php?rspec "RSpec Best Practices"){:target="_blank"}. In that article he recommends wrapping examples for each method in their own `describe` block with the method's name as the argument. In addition he recommends prefixing the method name with a "#" for instance methods and a "." for class methods for clarity. He also recommends using `context` to explain the scenarios that the method can be tested under. For example, our `withdraw` method can be executed when there are sufficient funds or when there are insufficient funds in the account.

Here's how the spec looks with these changes:

{% highlight ruby %}
require './bankaccount'

describe BankAccount do

  before :each do
    @account = BankAccount.new
  end

  describe "#initialize" do
    it "sets initial balance to zero" do
      @account.balance.should eq(0.00)
    end
  end

  describe "#deposit" do
    it "increases balance by amount of deposit" do
      @account.deposit 100.00
      @account.balance.should eq(100.00)
    end
  end

  describe "#withdraw" do
    context "when sufficient funds" do
      it "decreases balance by amount of withdrawal" do
        @account.deposit 100.00
        @account.withdraw 10.00
        @account.balance.should eq(90.00)
      end
    end
  end

end
{% endhighlight %}

Just to be sure that the test still works, let's run rspec again:

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  #initialize
    sets initial balance to zero
  #deposit
    increases balance by amount of deposit
  #withdraw
    when sufficient funds
      decreases balance by amount of withdrawal

Finished in 0.00134 seconds
3 examples, 0 failures
{% endhighlight %}

Oh, that's a bit more informative! Let's add our insufficient funds test now:

{% highlight ruby %}
require './bankaccount'

describe BankAccount do

  before :each do
    @account = BankAccount.new
  end

  describe "#initialize" do
    it "sets initial balance to zero" do
      @account.balance.should eq(0.00)
    end
  end

  describe "#deposit" do
    it "increases balance by amount of deposit" do
      @account.deposit 100.00
      @account.balance.should eq(100.00)
    end
  end

  describe "#withdraw" do
    context "when sufficient funds" do
      it "decreases balance by amount of withdrawal" do
        @account.deposit 100.00
        @account.withdraw 10.00
        @account.balance.should eq(90.00)
      end
    end

    context "when insufficient funds" do
      it "does not decrease balance" do
        @account.deposit 100.00
        @account.withdraw 200.00
        @account.balance.should eq(100.00)
      end
    end
  end

end
{% endhighlight %}

Will this test pass?

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  #initialize
    sets initial balance to zero
  #deposit
    increases balance by amount of deposit
  #withdraw
    when sufficient funds
      decreases balance by amount of withdrawal
    when insufficient funds
      does not decrease balance (FAILED - 1)

Failures:

  1) BankAccount#withdraw when insufficient funds does not decrease balance
     Failure/Error: @account.balance.should eq(100.00)

       expected: 100.0
            got: -100.0

       (compared using ==)
     # ./bankaccount_spec.rb:35:in `block (4 levels) in <top (required)>'

Finished in 0.00156 seconds
4 examples, 1 failure

Failed examples:

rspec ./bankaccount_spec.rb:32 # BankAccount#withdraw when insufficient funds does not decrease balance
{% endhighlight %}

That's helpful, RSpec even tells us what the expected and actual values were. Let's correct this oversight and retest:

{% highlight ruby %}
class BankAccount
  def initialize
    @balance = 0.00
  end

  def balance
    @balance
  end

  def deposit (amount)
    @balance += amount
  end

  def withdraw (amount)
    if @balance >= amount
      @balance -= amount
    end
  end
end
{% endhighlight %}

Now when we run the tests they should all pass:

{% highlight shell %}
$ rspec bankaccount_spec.rb --format documentation

BankAccount
  #initialize
    sets initial balance to zero
  #deposit
    increases balance by amount of deposit
  #withdraw
    when sufficient funds
      decreases balance by amount of withdrawal
    when insufficient funds
      does not decrease balance

Finished in 0.00156 seconds
4 examples, 0 failures
{% endhighlight %}

Hurray!

### Final Thoughts

Clearly I've just scratched the surface of what is possible with RSpec. It appears to be a very flexible unit testing tool that also provides useful test result documentation. Thankfully, Michael Hartl has interwoven BDD with RSpec throughout the Ruby on Rails Tutorial since it seems that this will be an invaluable tool for unit testing. 
