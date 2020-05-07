---
layout: post
title:      "Single Responsibility Principle in Class Methods"
date:       2020-05-07 16:16:50 +0000
permalink:  single_responsibility_principle_in_class_methods
---


When writing code for a program we should ensure that each class or module is responsible for a single piece of the program's functionality. Classes are like distinct entities that are each responsible for a specific purpose. It is logical then that all the class and instance methods in a class should be aligned to the responsibility of the particular class. Thus one should be careful not to write methods within a class that are not within the scope of the class. The class methods and by extension the instance methods should be written in such a way that it makes it easier to manage and even change later.The example below (source: https://thoughtbot.com/blog/back-to-basics-solid) shows a class that did not follow the single responsibility principle:

```
class DealProcessor
  def initialize(deals)
    @deals = deals
  end

  def process
    @deals.each do |deal|
      Commission.create(deal: deal, amount: calculate_commission)
      mark_deal_processed
    end
  end

  private

  def mark_deal_processed
    @deal.processed = true
    @deal.save!
  end

  def calculate_commission
    @deal.dollar_amount * 0.05
  end
end
```
The DealProcessor class is supposed to specifically process deals and not calculate commission. Therefore the code should be refactored so that we have two classes, each with a single separate responsibility. See below (source https://thoughtbot.com/blog/back-to-basics-solid)
```
class DealProcessor
  def initialize(deals)
    @deals = deals
  end

  def process
    @deals.each do |deal|
      mark_deal_processed
      CommissionCalculator.new.create_commission(deal)
    end
  end

  private

  def mark_deal_processed
    @deal.processed = true
    @deal.save!
  end
end

class CommissionCalculator
  def create_commission(deal)
    Commission.create(deal: deal, amount: deal.dollar_amount * 0.05)
  end
end
```
The single responsibility principle ensures that the code we write is logical and dry. When you find out that your code does not meet the single responsibility principle, it is time to refactor that code! 
