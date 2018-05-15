---
title: "Akka Typed: From Any => Unit To T => Behavior[T]"
date: 2018-05-15T11:13:58+02:00
draft: false
---

Akka Typed made a lot of progress over the last year and brings the great benefits of Scala's type system to Akka.

Here is a simple example of an immutable Actor which changes behaviour based on the incoming message.

```
object Greeter {
  sealed trait Command
  case object Greet extends Command
  final case class WhoToGreet(who: String) extends Command

  val greeterBehavior: Behavior[Command] = greeterBehavior(currentGreeting = "There is nobody to greet")

  private def greeterBehavior(currentGreeting: String): Behavior[Command] =
    Actor.immutable[Command] { (ctx, msg) =>
      msg match {
        case WhoToGreet(who) =>
          greeterBehavior(s"Hello, $who")
        case Greet =>
          println(currentGreeting)
          Actor.same
      }
    }
}
```
