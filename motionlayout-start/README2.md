
________________________________________________________________________________

                            FIRST COMMIT

________________________________________________________________________________

                              VIDEO 6

________________________________________________________________________________
Animations with MotionLayout

For this step you will build an animation that moves a view from
the top start of the screen to the bottom end in response to user clicks.

After you complete this step, you'll have implemented the following animation.

https://video.udacity-data.com/topher/2019/September/5d85326f_step1/step1.gif

The starter code for this step is missing several important elements
you will add.

Because of this, MotionLayout will not display this screen correctly
and you will see an empty screen or experience a crash until you
complete this step.

  To create the animation above with MotionLayout, you'll need the following
  major pieces

    * A MotionLayout which is a subclass of ConstraintLayout. You
      specify all the views to be animated in the MotionLayout tag.

    * A MotionScene which is an XML file that describes an animation
      for MotionLayout.

    * A Transition which is part of the MotionScene that specifies the
      animation duration, trigger, and how to move the views.

    * A ConstraintSet that specifies both the start and the end constraints
      of the transition.

Let's take a look at each of these in turn starting with the MotionLayout.

Introducing MotionLayout

  MotionLayout is a subclass of ConstraintLayout, so it supports all the
  same features while adding animation. To use MotionLayout, you just use
  a MotionLayout view where you would use ConstraintLayout

  In res/layout, open activity_step1.xml. Notice a MotionLayout with a
  single ImageView of a star with a tint applied inside of it.

          <!-- initial code -->
          <!-- activity_step1.xml -->
          <androidx.constraintlayout.motion.widget.MotionLayout
                 ...
                 android:layout_width="match_parent"
                 android:layout_height="match_parent"
                 >

             <ImageView
                     android:id="@+id/red_star"
                     ...
             />

          </androidx.constraintlayout.motion.widget.MotionLayout>

  This MotionLayout will behave the same as a full screen ConstraintLayout, but
  as of yet you haven't added any constraints. If you ran the app now,
  the screen would crash because you haven't added a MotionScene.

Add a MotionScene

  To animate using MotionLayout you need to specify a motion scene
  for the MotionLayout to use. This will let you describe the animation
  you want to build.

  A motion scene is a single XML file that describes an animation in
  a MotionLayout.

  For your layout to use a motion scene, it has to point at it.

`//TODO 1.1`
      1. Update your layout to point to a motion scene. Add an  app:layoutDescriptionattribute to the MotionLayout and point
      it to a MotionScene file which you will call @xml/step1.

          <!-- activity_step1.xml →
          <!-- add app:layoutDescription="@xml/step1" -->

          <androidx.constraintlayout.motion.widget.MotionLayout
                 ...
                 app:layoutDescription="@xml/step1">

  Important: Ensure that you add app:layoutDescription before continuing.

  Without the motion scene file, MotionLayout will not display this screen
  correctly and you will see an empty screen or experience a crash.

Declare a motion scene

`//TODO 1.2`
  1. To define the motion scene, create an XML file at res/xml/step1.xml and
     replace the default contents with this MotionScene tag and comments:

          <?xml version="1.0" encoding="utf-8"?>
          <!-- xml/step1.xml -->

          <MotionScene xmlns:app="http://schemas.android.com/apk/res-auto"
                      xmlns:android="http://schemas.android.com/apk/res/android">
              <!-- TODO: Define a Transition -->

              <!-- TODO: Define @id/start -->

              <!-- TODO: Define @id/end -->
          </MotionScene>

Define Start and End constraints

  All animations can be defined in terms of a start and an end. The start
  describes what the screen looks like before the animation, and the end
  describes what the screen looks like after the animation has completed.
  MotionLayout is responsible for figuring out how to animate between
  the start and end state (over time).

  MotionScene uses a ConstraintSet tag to define the start and end states.
  A ConstraintSet is what it sounds like, a set of constraints that can
  be applied to views. This includes width, height, and ConstraintLayout
  constraints. It also includes some attributes such as alpha. It doesn't
  contain the views themselves, just the constraints on those views.

  Any constraints specified in a ConstraintSet will override the constraints
  specified in the layout file. If you define constraints in both the
  layout and the MotionScene, only the constraints in the MotionScene
  are applied.

  A ConstraintSet is a child of <MotionScene> that defines a set of
  constraints that will be applied to one or more views declared in
  your layout file. These constraints can be used to define the start
  or the end of an animation.

  Constraint sets contain only contain the constraints or layout
  information such as width, height, alpha, or visibility. They don't
  contain other information such as the type of view or any view
  specific attributes like text on a TextView.

    In this exercise, you will constrain the star view to the top start
    of the screen to start, and the bottom end of the screen at the end.

`//TODO 1.3`
    1. Inside the MotionScene, replace the TODO for @id/start with the following ConstraintSet.

          <!-- xml/step1.xml -->
          <!-- TODO: Define @id/start -->

          <!-- Constraints to apply at the beginning of the animation -->
          <ConstraintSet android:id="@+id/start">
             <Constraint
                     android:id="@+id/red_star"
                     android:layout_width="wrap_content"
                     android:layout_height="wrap_content"
                     app:layout_constraintStart_toStartOf="parent"
                     app:layout_constraintTop_toTopOf="parent" />
          </ConstraintSet>

  The ConstraintSet has an ID of @id/start, and specifies all the constraints
  to apply to all the views in the MotionLayout. Since this MotionLayout
  only has one view, it only needs one Constraint.

  The Constraint inside the ConstraintSet specifies the id of the view
  that it's constraining, @id/red_star defined in activity_step1.xml.
  It's important to note that Constraint tags specify only constraints
  and layout information - the Constraint tag doesn't know that it's
  being applied to an ImageView.

  This constraint specifies the height, width, and the two other constraints
  needed to constrain the red_star view to the top start of its parent.

`//TODO 1.4`
    1. Next, specify the ConstraintSet for the end of the star animation in the MotionScene:

          <!-- xml/step1.xml →
          <!-- TODO: Define @id/end -->

          <!-- Constraints to apply at the end of the animation -->
          <ConstraintSet android:id="@+id/end">
             <Constraint
                     android:id="@+id/red_star"
                     android:layout_width="wrap_content"
                     android:layout_height="wrap_content"
                     app:layout_constraintEnd_toEndOf="parent"
                     app:layout_constraintBottom_toBottomOf="parent" />
          </ConstraintSet>

  Just like @id/start, this ConstraintSet has a single Constraint
  on @id/red_star. This time it constrains it to the bottom end
  of the screen.

  You don't have to name them @id/start and @id/end, but it is convenient
  to do so.

  When using MotionLayout, you should specify the constraints of any views
  that are animated in the motion scene XML file instead of the layout.
  Any views that are not animated may be constrained in the layout
  instead of the motion scene.

Define a Transition

  Every MotionScene must also include at least one transition. A transition
  defines every part of one animation, from start to end.

  A transition must specify a start and end ConstraintSet for the transition.
  In addition, a transition can specify how to modify the animation in
  other ways, such as how long to run the animation or how to animate
  by dragging views.

`//TODO 1.5`
    1. Inside the MotionScene, replace the TODO to define a transition:

          <!-- xml/step1.xml -->
          <!-- TODO: Define a Transition -->

          <!-- A transition describes an animation via start and end state -->
          <Transition
              app:constraintSetStart="@+id/start"
              app:constraintSetEnd="@+id/end"
              app:duration="2000">
              <!-- TODO: Handle clicks -->
          </Transition>

  This is everything that MotionLayout needs to build an animation.
  Looking at each attribute:

    *constraintSetStart will be applied to the views as the animation starts

    *constraintSetEnd will be applied to the views at the end of the animation

    *duration specifies how long the animation should take (ms)

  MotionLayout will then figure out a path between the start and
  end constraints and animate it for the specified duration.

  We need a way to start the animation. One way to do this is to make
  the MotionLayout respond to click events on @id/red_star.

`//TODO 1.5`
    1. To make MotionLayout respond to click events update the transition
       to have an OnClick tag.

          <!-- xml/step1.xml -->
          <!-- TODO: Handle clicks -->

          <!-- A transition describes an animation via start and end state -->
          <Transition
              app:constraintSetStart="@+id/start"
              app:constraintSetEnd="@+id/end"
              app:duration="2000">
              <!-- MotionLayout will handle clicks on @id/red_star to "toggle" the animation between the start and end -->
              <OnClick
                  app:targetId="@id/red_star"
                  app:clickAction="toggle" />
          </Transition>

  The Transition tells MotionLayout to run the animation in response to
  click events using an <OnClick> tag. Looking at each attribute:

    * targetId' is the view to watch for clicks

    * 'clickAction' of toggle will switch between the start and end state on
      click, you can see other options for clickAction in the documentation

    * Run your code, click Step 1, then click the red star and see the animation!

  A Transition describes one animation in a MotionScene. It contains the
  specification for a complete animation to MotionLayout, including all
  views that change during the animation, how long the animation should
  take, and how to handle user touch to drive the animation.

  A MotionScene can have more than one animation and more than one Transition.

    Note: It is possible to load a ConstraintSet from an existing
          ConstraintLayout by pointing start or end to a layout file instead
          of a ConstraintSet. However, we don't recommend this as it's harder
          to keep the code in sync between multiple files.

Animations in action

  If you run the app, you see your animation running when you click on the star.

  https://video.udacity-data.com/topher/2019/October/5d964f71_step1/step1.gif


  The completed motion scene file defines one Transition which points
  to a start and end ConstraintSet.

  At the start of the animation (@id/start), the star icon is constrained
  to the top start of the screen. At the end of the animation (@id/end)
  the star icon is constrained to the bottom end of the screen.

          <?xml version="1.0" encoding="utf-8"?>
          <!-- Describe the animation for activity_step1.xml -->
          <MotionScene xmlns:app="http://schemas.android.com/apk/res-auto"
                      xmlns:android="http://schemas.android.com/apk/res/android">
             <!-- A transition describes an animation via start and end state -->
             <Transition
                     app:constraintSetStart="@+id/start"
                     app:constraintSetEnd="@+id/end"
                     app:duration="2000">
                 <!-- MotionLayout will handle clicks on @id/star to "toggle" the animation between the start and end -->
                 <OnClick
                         app:targetId="@id/red_star"
                         app:clickAction="toggle" />
             </Transition>

             <!-- Constraints to apply at the end of the animation -->
             <ConstraintSet android:id="@+id/start">
                 <Constraint
                         android:id="@+id/red_star"
                         android:layout_width="wrap_content"
                         android:layout_height="wrap_content"
                         app:layout_constraintStart_toStartOf="parent"
                         app:layout_constraintTop_toTopOf="parent" />
             </ConstraintSet>

             <!-- Constraints to apply at the end of the animation -->
             <ConstraintSet android:id="@+id/end">
                 <Constraint
                         android:id="@+id/red_star"
                         android:layout_width="wrap_content"
                         android:layout_height="wrap_content"
                         app:layout_constraintEnd_toEndOf="parent"
                         app:layout_constraintBottom_toBottomOf="parent" />
             </ConstraintSet>
          </MotionScene>


________________________________________________________________________________

                              VIDEO 7

________________________________________________________________________________


FIRST VIDEO

Animating based on drag events

  For this step, you will build an animation that responds to a user drag
  event (such as when the user swipes the screen) to run the animation.
  Motionlayout supports tracking touch events to move views, as well
  as physics-based fling gestures to make the motion fluid.

  After you complete this step, you'll have implemented the following
  animation that responds to touch.

  https://video.udacity-data.com/topher/2019/October/5d975429_step2/step2.gif

SECOND VIDEO

Inspect the initial code

    1. To get started, open the layout file activity_step2.xml, which has
       an existing MotionLayout. Take a look at the code.
          <!-- initial code in activity_step2.xml -->
          <androidx.constraintlayout.motion.widget.MotionLayout
                 ...
                 app:layoutDescription="@xml/step2" >

             <ImageView
                     android:id="@+id/left_star"
                     ...
             />

             <ImageView
                     android:id="@+id/right_star"
                     ...
             />

             <ImageView
                     android:id="@+id/red_star"
                     ...
             />

             <TextView
                     android:id="@+id/credits"
                     ...
                     app:layout_constraintTop_toTopOf="parent"
                     app:layout_constraintEnd_toEndOf="parent"/>
          </androidx.constraintlayout.motion.widget.MotionLayout>

  This layout defines all the views for the animation. The three star
  icons are not constrained in the layout because they will be
  animated in the motion scene.

  The credits TextView does have constraints applied, because it stays
  in the same place for the entire animation and doesn't modify any attributes.

  Views that are not animated by a MotionLayout animation should specify
  their constraints in the layout XML file. MotionLayout will not modify
  constraints that aren't referenced by a <Constraint> in the <MotionScene>.

  Views that are animated should have their constraints set in the motion
  scene XML file.

Animating the scene

  Just like the last animation, the animation will be defined by a start
  and end ConstraintSet, and a Transition.

Define the start ConstraintSet

    1. Open the motion scene xml/step2.xml to define the animation.

`//TODO 1.6`
    2. Add the constraints for the starting constraint start. At the start,
       all three stars are centered at the bottom of the screen. The right
       and left stars have an alpha value of 0.0, which means that they're
       fully transparent and hidden.

          <!-- xml/step2.xml →
          <!-- TODO apply starting constraints -->
          <!-- Constraints to apply at the start of the animation -->
          <ConstraintSet android:id="@+id/start">
             <Constraint
                     android:id="@+id/red_star"
                     android:layout_width="wrap_content"
                     android:layout_height="wrap_content"
                     app:layout_constraintStart_toStartOf="parent"
                     app:layout_constraintEnd_toEndOf="parent"
                     app:layout_constraintBottom_toBottomOf="parent" />

             <Constraint
                     android:id="@+id/left_star"
                     android:layout_width="wrap_content"
                     android:layout_height="wrap_content"
                     android:alpha="0.0"
                     app:layout_constraintStart_toStartOf="parent"
                     app:layout_constraintEnd_toEndOf="parent"
                     app:layout_constraintBottom_toBottomOf="parent" />

             <Constraint
                     android:id="@+id/right_star"
                     android:layout_width="wrap_content"
                     android:layout_height="wrap_content"
                     android:alpha="0.0"
                     app:layout_constraintStart_toStartOf="parent"
                     app:layout_constraintEnd_toEndOf="parent"
                     app:layout_constraintBottom_toBottomOf="parent" />
          </ConstraintSet>

  In this ConstraintSet you specify one Constraint for each of the stars.
  Each constraint will be applied by MotionLayout at the start of the
  animation.

  Each star view is centered at the bottom of the screen using start, end,
  and bottom constraints. The two stars @id/left_star and @id/right_star both
  have an additional alpha value that makes them invisible and that will be
  applied at the start of the animation.

  Note: The start and end constraint sets define the start and end
        of the animation. A constraint on the start, like
        app:layout_constraintStart_toStartOf will constrain a view's start
        to the start of another view. This can be confusing at first because
        the name start is used for both and they're both used in the context
        of constraints. To help draw out the distinction, the start in
        layout_constraintStart refers to the "start" of the view, which
        is the left in a left to right language and right in a right to
        left language. The start constraint set refers to the start of
        the animation..

  You can specify an alpha value in a Constraint. This value determines
  the transparency of the view, where '"0.0"' is fully transparent and
  '"1.0"' is fully opaque.

  When animating between two alpha values, MotionLayout will smoothly
  transition between them. For example, when animating between
  alpha="0.0" and alpha="1.0", MotionLayout will create a fade-in effect.

Define the end ConstraintSet

`//TODO 1.7`
    1. Define the end constraint to set use a chain to position all three
       stars together below @id/credits. In addition, it will set the end
       value of the alpha of the left and right stars to 1.0.

          <!-- xml/step2.xml →
          <!-- TODO apply ending constraints →

          <!-- Constraints to apply at the end of the animation -->
          <ConstraintSet android:id="@+id/end">

             <Constraint
                     android:id="@+id/left_star"
                     android:layout_width="wrap_content"
                     android:layout_height="wrap_content"
                     android:alpha="1.0"
                     app:layout_constraintHorizontal_chainStyle="packed"
                     app:layout_constraintStart_toStartOf="parent"
                     app:layout_constraintEnd_toStartOf="@id/red_star"
                     app:layout_constraintTop_toBottomOf="@id/credits" />

             <Constraint
                     android:id="@+id/red_star"
                     android:layout_width="wrap_content"
                     android:layout_height="wrap_content"
                     app:layout_constraintStart_toEndOf="@id/left_star"
                     app:layout_constraintEnd_toStartOf="@id/right_star"
                     app:layout_constraintTop_toBottomOf="@id/credits" />

             <Constraint
                     android:id="@+id/right_star"
                     android:layout_width="wrap_content"
                     android:layout_height="wrap_content"
                     android:alpha="1.0"
                     app:layout_constraintStart_toEndOf="@id/red_star"
                     app:layout_constraintEnd_toEndOf="parent"
                     app:layout_constraintTop_toBottomOf="@id/credits" />
          </ConstraintSet>


   The end result is that the views will spread out and up from the center
   as they animate.

  In addition, since the alpha property is set on @id/right_start and
  @id/left_star in both ConstraintSets, both views will fade in as the
  animation progresses.

Animating based on user swipe

  MotionLayout can track user drag events, or a swipe, to create a
  physics-based "fling" animation. This means the views will keep going
  if the user flings them and will slow down like a physical object
  would when rolling across a surface. You can add this type
  of animation with an OnSwipe tag in the Transition.

`//TODO 1.8`
    1. Replace the TODO for adding an OnSwipe tag with
       <OnSwipe app:touchAnchorId="@id/red_star" />.

          <!-- xml/step2.xml -->
          <!-- TODO add OnSwipe tag -->

          <!-- A transition describes an animation via start and end state -->
          <Transition
                 app:constraintSetStart="@+id/start"
                 app:constraintSetEnd="@+id/end">
             <!-- MotionLayout will track swipes relative to this view -->
             <OnSwipe app:touchAnchorId="@id/red_star" />
          </Transition>

  OnSwipe contains a few attributes, the most important being touchAnchorId.

    * touchAnchorId - the tracked view that moves in response to touch.
      MotionLayout will keep this view the same distance from the finger
      that's swiping.

    * touchAnchorSide - which side of the view should be tracked. This is
      important for views that resize, follow complex paths, or have one
      side that moves faster than the other.

    * dragDirection - which direction matters for this
      animation (up, down, left or right)

  When MotionLayout listens for drag events, the listener will be
  registered on the MotionLayout view and not the view specified
  by touchAnchorId. When a user starts a gesture anywhere on the
  screen, MotionLayout will keep the distance between their finger
  and the touchAnchorSide of the touchAnchorId view constant. If they
  touch 100dp away from the anchor side, for example, MotionLayout will
  keep that side 100dp away from their finger for the entire animation.

  OnSwipe listens for swipes on the MotionLayout and not the view specified
  in touchAnchorId.

  This means the user may swipe outside of the specified view to run
  the animation.

Try it out

  1. Run the app again, and open the Step 2 screen. You will see the animation.

  2. Try "flinging" or releasing your finger halfway through the animation
     to explore how MotionLayout displays fluid physics based animations!

     https://video.udacity-data.com/topher/2019/October/5d975429_step2/step2.gif

  MotionLayout can animate between very different designs using the
  features from ConstraintLayout to create rich effects.

  In this animation, all three views are positioned relative to their parent
  at the bottom of the screen to start. At the end, the three views are
  positioned relative to @id/credits in a chain.

  Despite these very different layouts, MotionLayout will create a fluid
  animation between start and end.

________________________________________________________________________________

                              VIDEO 8
________________________________________________________________________________



Modifying a path

  In this step you will build an animation that follows a complex
  path during the animation and animates the credits during the
  motion. MotionLayout can modify the path that a view will take
  between the start and the end using a KeyPosition.

  After you complete this step, you'll have implemented the following
  animation driven by clicking on the moon.

https://video.udacity-data.com/topher/2019/October/5d97568c_step3/step3.gif

FIRST VIDEO

Explore the existing code

    1. Open layout/activity_step3.xml and xml/step3.xml to see the existing
       layout and motion scene.

    2. An ImageView and TextView display the moon and credits text. Open the
       motion scene file (xml/step3.xml).

  You see that a Transition from @id/start to @id/end is defined. The
  animation moves the moon image from the lower left of the screen
  to the bottom right of the screen using two ConstraintSets. The
  credits text fades in from alpha="0.0" to alpha="1.0" as the moon
  is moving.

    3. Run the app now and select Step 3. You'll see that the
       moon follows a linear path (or a straight line) from start
       to end when you click on the moon.

Enabling path debugging

  Before you add an arc to the moon's motion, it's helpful to enable
  path debugging in MotionLayout.

  To help develop complex animations with MotionLayout, you can draw
  the animation path of every view. This is helpful when you want to
  visualize your animation at a glance, and for fine tuning the
  small details of motion.

`//TODO 1.9`
    1. To enable debugging paths, open layout/activity_step3.xml and add  app:motionDebug="SHOW_PATH" to the MotionLayout tag.

          <!-- layout/activity_step3.xml -->
          <!-- Add app:motionDebug="SHOW_PATH" -->

          <androidx.constraintlayout.motion.widget.MotionLayout
                 ...
                 app:motionDebug="SHOW_PATH" >

https://video.udacity-data.com/topher/2019/October/5d97571a_step3-flat-annotated/step3-flat-annotated.png

  After you enable path debugging, when you run the app again you'll
  see the paths of all views visualized with a dotted line.

    * Circles - represent the start or end position of one view

    * Lines - represent the path of one view

    * Diamonds - represent a KeyPosition that modifies the path

  For example, in this animation, the middle circle is the position of
  the credits text.

Modifying a path

  All animations in MotionLayout are defined by a start and end
  ConstraintSet that define what the screen looks like before
  the animation starts and after the animation is done. By default,
  MotionLayout will plot a linear path (or a straight line) between
  the start and end position of each view that changes position.

  To build complex paths like the arc of the moon in this example,
  MotionLayout uses a KeyPosition to modify the path that a view
  takes between the start and end.

  A KeyPosition modifies the path a view takes between the start and
  the end ConstraintSet.

  It can distort the path of a view to go through a third
  (or fourth, or fifth, …) point between the start and end
  positions. Or, it can even speed up and slow down progress
  along either the X or Y axis.

  A KeyPosition can only change the path during the animation, it cannot
  change the start or the end.

  The ConstraintSet will always specify the final position for the views
  at the start and end of the animation.

    1. Open xml/step3.xml and add a KeyPosition to the scene.

`//TODO 1.10`
https://video.udacity-data.com/topher/2019/October/5d9757a7_step3-curved-annotated/step3-curved-annotated.png

          <!-- xml/step3.xml -->
          <!-- TODO: Add KeyFrameSet and KeyPosition -->
          <KeyFrameSet>
             <KeyPosition
                     app:framePosition="50"
                     app:motionTarget="@id/moon"
                     app:keyPositionType="parentRelative"
                     app:percentY="0.5"
             />
          </KeyFrameSet>

  A KeyFrameSet is a child of a Transition, and it is a set of all
  the KeyFrames, such as KeyPosition, that should be applied during
  the transition.

  As MotionLayout is calculating the path for the moon between the start
  and the end, it modifies the path based on the KeyPosition specified
  in the KeyFrameSet. You can see how this modifies the path by running
  the app again.

  A KeyPosition has several attributes that describe how it modifies
  the path, the most important ones are:

    * framePosition - a number between 0 and 100 to say when in the animation
      this  KeyPosition should be applied, with 1 being 1% through the
      animation, and 99 being 99% through the animation. So if the value
      is 50, we apply it right in the middle.

    * motionTarget - the view for which this KeyPosition modifies the path

    * keyPositionType - how this KeyPosition modifies the path. It can
      be either parentRelative, pathRelative, or
      deltaRelative (explained in the next step).

    * percentX | percentY - how much to modify the path at
      framePosition (values between 0.0 and 1.0, with negative values
      and values >1 allowed)

  You can think of it this way, "At framePosition modify the path
  of motionTarget by moving it by percentX or percentY" according
  to the coordinates determined by keyPositionType."

  By default MotionLayout will round any corners that are introduced by
  modifying the path. If you look at the animation you just
  created, you can see the moon follows a curved path at the bend.
  For most animations, this is what you want, and if not you can
  specify the curveFit attribute to customize it.

Try it out

  If you run the app again, you'll see the animation for this step.

https://video.udacity-data.com/topher/2019/October/5d97568c_step3/step3.gif

  The moon follows an arc because it goes through a KeyPosition specified
  in the Transition.

          <KeyPosition
                 app:framePosition="50"
                 app:motionTarget="@id/moon"
                 app:keyPositionType="parentRelative"
                 app:percentY="0.5"
          />

  You can read this KeyPosition as, "At framePosition 50 (halfway through
  the animation) modify the path of motionTarget @id/moon by moving
  it by 50% Y (halfway down the screen) according to the coordinates
  determined by parentRelative (the entire MotionLayout)."

  So, half way through the animation, the moon must go through a
  KeyPosition that's 50% down on the screen. This KeyPosition
  doesn't modify the X motion at all, so the moon will still
  go from start to end horizontally. MotionLayout will figure
  out a smooth path that goes through this KeyPosition and while
  moving between start and end.

  If you look closely, the credits text is constrained by the position
  of the moon. Why isn't it moving vertically as well?

https://video.udacity-data.com/topher/2019/October/5d975889_step3-zoom/step3-zoom.gif

          <Constraint
                 android:id="@id/credits"
                 ...
                 app:layout_constraintBottom_toBottomOf="@id/moon"
                 app:layout_constraintTop_toTopOf="@id/moon"
          />

  It turns out, even though we're modifying the path that the moon
  takes, the start and end positions of the moon don't move it
  vertically at all. The KeyPosition doesn't modify the start or
  the end position, so the credits text is constrained to the
  final end position of the moon.

  If you did want the credits to move with the moon, you could
  add a KeyPosition to the credits, or modify the start
  constraints on @id/credits.

  Start and end constraints are never modified by a KeyPosition.

  Even if a view is following a complex motion path, like @id/moon,
  the start and end constraints will always rest at their initial
  or final positions. Other views constrained to @id/moon will
  not follow the path in between.

  In the next section we'll dive into the different types
  of keyPositionType in MotionLayout.


________________________________________________________________________________

                          VIDEO 10

________________________________________________________________________________


Building complex paths

  Looking at the animation you built in the last step, it does create
  a smooth curve - but the shape could be more "moon like."

  In this step, you will modify the transition to round out the motion
  of the moon to create a more "moon like" arc.

https://video.udacity-data.com/topher/2019/October/5d976e36_image2/image2.gif


Modifying a path with multiple KeyPosition elements

  MotionLayout can modify a path further by defining as many KeyPosition
  as needed to get any motion. For this animation you will build an
  arc, but you could make the moon jump up and down in the middle of
  the screen if you wanted.

    1. Open xml/step4.xml. You see it has the same views and the KeyFrame you
       added in the last step.

`//TODO 1.11`
    2. To round out the top of the curve, add two more KeyPositions to the
       path of @id/moon, one just before it reaches the top and one after.

https://video.udacity-data.com/topher/2019/October/5d976e65_image6/image6.png

          <!-- xml/step4.xml -->
          <!-- TODO: Add two more KeyPositions to the KeyFrameSet here -->
          <KeyPosition
                 app:framePosition="25"
                 app:motionTarget="@id/moon"
                 app:keyPositionType="parentRelative"
                 app:percentY="0.6"
          />
          <KeyPosition
                 app:framePosition="75"
                 app:motionTarget="@id/moon"
                 app:keyPositionType="parentRelative"
                 app:percentY="0.6"
          />

  These KeyPositions will be applied 25% and 75% of the way through
  the animation, and cause @id/moon to move through a path that is
  60% from the top of the screen. Combined with the existing
  KeyPosition at 50%, this creates a smooth arc for the moon to follow.

  In MotionLayout, you can add as many KeyPositions as you would need
  to get the motion path you want. MotionLayout will apply each
  KeyPosition at the specified framePosition, and figure out how
  to create a smooth motion that goes through all of the KeyPositions.

  A KeyPosition always defines an (x, y, width, height) position that
  the View must move through during the transition from start to end.

  If you don't specify one dimension, it will have a default
  value (zero, or an appropriate value based on the framePosition).
  In this example, by specifying only percentY, the percentX keeps
  its default value for that keyPosition.

Run the animation

    1. Run the app again. Go to Step 4 to see the animation in action.
       When you click on the moon, it follows the path from start
       to end – going through each KeyPosition that was specified in
       the KeyFrameSet.

  Modifying a path with several KeyPositon tags allows you to build
  complex motion.

  You can build arcs, configure sharp corners, make views bounce
  around, or hop from start to end. Since MotionLayout lets you
  apply several KeyPositions to the same path, you can modify
  the path a view takes from start to end dramatically.

Explore on your own

    1. Before you move on to other types of KeyFrames, try adding some
       more KeyPositions to the KeyFrameSet to see what kind of
       effects you can create just using KeyPosition. Here's one
       example showing how to build a complex path that moves
       back and forth during the animation.

https://video.udacity-data.com/topher/2019/October/5d976ec7_image5/image5.png

          <!-- Complex paths example: Dancing moon -->
          <KeyFrameSet>
             <KeyPosition
                     app:framePosition="25"
                     app:motionTarget="@id/moon"
                     app:keyPositionType="parentRelative"
                     app:percentY="0.6"
                     app:percentX="0.1"
             />
             <KeyPosition
                     app:framePosition="50"
                     app:motionTarget="@id/moon"
                     app:keyPositionType="parentRelative"
                     app:percentY="0.5"
                     app:percentX="0.3"
             />
             <KeyPosition
                     app:framePosition="75"
                     app:motionTarget="@id/moon"
                     app:keyPositionType="parentRelative"
                     app:percentY="0.6"
                     app:percentX="0.1"
             />
          </KeyFrameSet>

Once your done exploring KeyPosition, in the next step you'll move
on to other types of KeyFrames.


________________________________________________________________________________

                              VIDEO 11

________________________________________________________________________________




Changing attributes during motion

  Building dynamic animations often means changing the size, rotation, or
  alpha of views as the animation progresses. MotionLayout supports
  animating many attributes on any view using a KeyAttribute.

  In this step, you will use KeyAttributes to make the moon scale
  and rotate. You will also use a KeyAttribute to delay the
  appearance of the text until the moon has almost
  completed its journey.

  After you have completed this step, you will have created
  the following animation.

https://video.udacity-data.com/topher/2019/October/5d976fc6_image7/image7.gif

Resize and Rotate with KeyAttribute

    1. Open xml/step5.xml which contains the same animation you built in
       the last step. For variety, this screen uses a different space
       picture as the background.

`//TODO 1.12`
    2. To make the moon expand in size and rotate, add two
       KeyAttributes in the KeyFrameSet at keyFrame="50" and keyFrame="100"

https://video.udacity-data.com/topher/2019/October/5d977001_image20/image20.png

          <!-- xml/step5.xml -->

          <!-- TODO: Add KeyAttributes to rotate and resize @id/moon -->

          <!-- KeyAttributes modify attributes during motion -->
          <KeyAttribute
                 app:framePosition="50"
                 app:motionTarget="@id/moon"
                 android:scaleY="2.0"
                 android:scaleX="2.0"
                 android:rotation="-360"
          />
          <KeyAttribute
                 app:framePosition="100"
                 app:motionTarget="@id/moon"
                 android:rotation="-720"
          />

  These KeyAttributes are applied at 50% and 100% of the animation.
  The first KeyAttribute at 50% will happen at the top of the arc, and
  causes the view to be doubled in size as well as rotate
  -360 degrees (or one full circle). The second KeyAttribute will
  finish the second rotation to -720 degrees (two full circles) and
  shrink the size back to regular since the scaleX and scaleY values
  default to 1.0.

  Just like a KeyPosition, a KeyAttribute uses the framePosition
  and motionTarget to specify when to apply the KeyFrame and which
  view to modify. MotionLayout will interpolate between KeyPositions
  to create fluid animations.

  KeyAttributes support attributes that can be applied to all
  views. They support changing basic attributes such as the
  visibility, alpha, or elevation. You can also change the
  rotation like we're doing here, rotate in three dimensions
  with rotateX and rotateY, scale the size with scaleX and
  scaleY, or translate the view's position in X Y or Z.

  Multiple attributes can be modified at the same time by
  a single KeyAttribute.

  In this animation, the KeyAttribute at keyFrame="50" sets
  scaleX, scaleY, and rotation. All three attributes will
  be modified at the same time by MotionLayout.

Delay the appearance of credits

  One of the goals of this step is to update the animation so
  that the credits text doesn't appear until the animation
  is mostly complete.

`//TODO 1.13`
    1. To delay the appearance of credits, define one more KeyAttribute
       that ensures that alpha will remain 0 until keyPosition="85".
       MotionLayout will still smoothly transition from 0 to 100 alpha, but
       it will do it over the last 15% of the animation.

          <!-- xml/step5.xml -->

          <!-- TODO: Add KeyAttribute to delay the appearance of @id/credits -->

          <KeyAttribute
                 app:framePosition="85"
                 app:motionTarget="@id/credits"
                 android:alpha="0.0"
          />

  This KeyAttribute keeps the alpha of@id/credits at 0.0 for the
  first 85% of the animation. Since it starts at an
  alpha of 0, this means it will be invisible for the
  first 85% of the animation.

  The end effect of this KeyAttribute is that the credits appear towards
  the end of the animation. This gives the appearance of them being
  coordinated with the moon settling down in the right corner of the screen.

  By delaying animations on one view while another view moves like
  this, you can build impressive animations that feel dynamic to the user.

  A KeyAttribute will never change the appearance of a view at the
  start or end position.

  If a view is rotated, translated, or scaled at framePosition="100"
  (or 100% through the animation), it will "jump" to its final value.
  To change the starting or end states, modify the Constraints
  in the ConstraintSet.

Try out the animation

    1. Run the app again and go to Step 5 to see the animation in action.
       When you click on the moon, it'll follow the path from start to
       end – going through each KeyAttribute that was specified in
       the KeyFrameSet.

https://video.udacity-data.com/topher/2019/October/5d976fc6_image7/image7.gif

  Because we rotate the moon two full circles, it will now do a
  double back flip, and the credits will delay their appearance
  until the animation is almost done.

Explore on your own

    1. Before you move on to the final type of KeyFrame, try modifying
       other standard attributes in the KeyAttributes. For example,
       try changing rotation to rotationX to see what animation it produces.

  Here's a list of the standard attributes that you can try:

    * android:visibility
    * android:alpha
    * android:elevation
    * android:rotation
    * android:rotationX
    * android:rotationY
    * android:scaleX
    * android:scaleY
    * android:translationX
    * android:translationY
    * android:translationZ

________________________________________________________________________________

                                VIDEO 12

________________________________________________________________________________



Changing attributes during motion

  Rich animations involve changing the color or other attributes of
  a view. While MotionLayout can use a KeyAttribute to change any of
  the standard attributes listed in the previous task, you use a
  CustomAttribute to specify any other attribute.

  A CustomAttribute can be used to set any value that has a setter.
  For example, you can set the backgroundColor on a View using a
  CustomAttribute. MotionLayout will use reflections to find the
  setter, then call it repeatedly to animate the view.

  In this step, you will use a CustomAttribute to set the colorFilter
  attribute on the moon to build the animation shown below.

https://video.udacity-data.com/topher/2019/October/5d977177_image17/image17.gif


Defining custom attributes

    1. To get started open xml/step6.xml which contains the same
       animation you built in the last step.

`//TODO 1.14`
    2. To make the moon change colors, add two KeyAttribute with
       a CustomAttribute in the KeyFrameSet at keyFrame="0", keyFrame="50" and keyFrame="100"

https://video.udacity-data.com/topher/2019/October/5d97719a_image4/image4.png

          <!-- xml/step6.xml -->

          <!-- TODO: Add Custom attributes here -->
          <KeyAttribute
                 app:framePosition="0"
                 app:motionTarget="@id/moon">
             <CustomAttribute
                     app:attributeName="colorFilter"
                     app:customColorValue="#FFFFFF"
             />
          </KeyAttribute>
          <KeyAttribute
                 app:framePosition="50"
                 app:motionTarget="@id/moon">
             <CustomAttribute
                     app:attributeName="colorFilter"
                     app:customColorValue="#FFB612"
             />
          </KeyAttribute>
          <KeyAttribute
                 app:framePosition="100"
                 app:motionTarget="@id/moon">
             <CustomAttribute
                     app:attributeName="colorFilter"
                     app:customColorValue="#FFFFFF"
             />
          </KeyAttribute>

  You add a CustomAttribute inside a KeyAttribute. TheCustomAttribute
  will be applied at the framePosition specified by the KeyAttribute.

  Inside the CustomAttribute you must specify an attributeName
  and one value to set.

    * app:attributeName - the name of the setter that will be called by
                          this custom attribute. In this example
                          setColorFilter on Drawable will be called.

    * app:custom*Value - A custom value of the type noted in the name, in
                         this example the custom value is a color specified.

  Custom values can have any of the following types:

    * Color
    * Integer
    * Float
    * String
    * Dimension
    * Boolean

  Using this API, MotionLayout can animate anything that provides a setter
  on any view.

  Custom views can be animated using a CustomAttribute.

  As long as MotionLayout can find a setter that takes the correct type
  it can animate changes between values.

Try out the animation

    1. Run the app again and go to Step 6 to see the animation in action.
       When you click on the moon, it'll follow the path from start to
       end – going through each KeyAttribute that was specified in
       the KeyFrameSet.

https://video.udacity-data.com/topher/2019/October/5d977177_image17/image17.gif

  When you add more KeyFrames, MotionLayout changes the path of the moon
  from a straight line to a complex curve, adding a double backflip,
  resize, and a color change midway through the animation.

  In real animations, you'll often animate several views at the same time
  controlling their motion along different paths and speeds. By specifying
  a different KeyFrame for each view, it's possible to choreograph rich
  animations that animate multiple views with MotionLayout.


________________________________________________________________________________

                            VIDEO 13

______________________________________________________________________________



Drag events and complex paths

  In this step you'll explore using OnSwipe with complex paths.
  So far, the animation of the Moon has been triggered by
  an OnClick listener and run for a fixed duration.

  Controlling animations that have complex paths, like the moon
  animation you've built in the last few steps, using OnSwipe
  requires understanding how OnSwipe works.

Exploring OnSwipe behavior

    1. Open xml/step7.xml and find the existing OnSwipe declaration.

          <!-- xml/step7.xml -->

          <!-- Fix OnSwipe by changing touchAnchorSide -->
          <OnSwipe
                 app:touchAnchorId="@id/moon"
                 app:touchAnchorSide="bottom"
          />

    2. Run the app on your device and go to Step 7. See if you can
       produce a smooth animation by dragging the moon along the
       path of the arc.

  When you run this animation, it doesn't look very good. After the
  moon reaches the top of the arc, it starts jumping around.

https://video.udacity-data.com/topher/2019/October/5d97731b_image11/image11.gif

  To understand the bug, consider what happens when the user is
  touching just below the top of the arc. Because the OnSwipe
  tag has an app:touchAnchorSide="bottom" MotionLayout will
  try to make the distance between the finger and the
  bottom of the view constant throughout the animation.

  But, since the bottom of the moon doesn't always go in the same
  direction, it goes up then comes back down, MotionLayout
  doesn't know what to do when the user has just passed the
  top of the arc. To consider this, since we're tracking
  the bottom of the moon where should it be placed when
  the user is touching here?

https://video.udacity-data.com/topher/2019/October/5d977352_image18/image18.png

Using the right side

  To avoid bugs like this, it is important to always choose a
  touchAnchorId and touchAnchorSide that always progresses
  in one direction throughout the duration of the entire
  animation.

  In this animation, both the right side and the left side of the
  moon will progress across the screen in one direction.

  However, both the bottom and the top will reverse direction.
  When OnSwipe attempts to track them, it will get confused
  when their direction changes.

`//TODO 1.15`
    1. To make this animation follow touch events, change the
       touchAnchorSide to right.

          <!-- xml/step7.xml -->

          <!-- Fix OnSwipe by changing touchAnchorSide -->
          <OnSwipe
                 app:touchAnchorId="@id/moon"
                 app:touchAnchorSide="right"
          />

  The touchAnchorSide passed to OnSwipe must progress in a single
  direction through the entire animation.

  If the anchored side reverses its path, or pauses, MotionLayout
  will get confused and not progress in a smooth motion.

  In some animations, no view has an appropriate touchAnchorSide.

  This may happen if every side follows a complex path through the
  motion or views resize in ways that would cause surprising
  animations. In these situations, consider adding an
  invisible view that follows a simpler path to track.

Using dragDirection

  You can also combine dragDirection with touchAnchorSide to make
  a side track a different direction than it normally would.
  It's still important that the touchAnchorSide only
  progress in one direction, but you can tell
  MotionLayout which direction to track. For example,
  you can keep the touchAnchorSide="bottom" but add
  dragDirection="dragRight". This will cause MotionLayout to
  track the position of the bottom of the view, but only consider
  its location when moving right (it ignores vertical motion). So, even
  though the bottom goes up and down, it will still animate correctly
  with OnSwipe.

`//TODO 1.16`
    1. Update OnSwipe will to track the moon's motion correctly.

          <!-- xml/step7.xml -->

          <!-- Using dragDirection to control the direction of drag tracking -->
          <OnSwipe
                 app:touchAnchorId="@id/moon"
                 app:touchAnchorSide="bottom"
                 app:dragDirection="dragRight"
          />

Run the animation

    1. Run the app again and try dragging the moon through the entire path.
       Even though it follows a complex arc, MotionLayout will be able
       to progress the animation in response to swipe events.

https://video.udacity-data.com/topher/2019/October/5d9773b5_image13/image13.gif


______________________________________________________________________________

                            VIDEO 14

______________________________________________________________________________


Running motion with code

  MotionLayout can be used to build rich animations when used with
  CoordinatorLayout. In this step, you'll build a collapsible
  header using MotionLayout.

  After you complete this step you'll have built this animation.

https://video.udacity-data.com/topher/2019/October/5d977428_image19/image19.gif


Explore the existing code

    1. To get started, open layout/activity_step8.xml.

    2. In layout/activity_step8.xml,you see that a working
       CoordinatorLayout and AppBarLayout is already built.
          <!-- layout/activity_step8.xml -->

          <androidx.coordinatorlayout.widget.CoordinatorLayout
                 ...>
             <com.google.android.material.appbar.AppBarLayout
                     android:id="@+id/appbar_layout"
                     android:layout_width="match_parent"
                     android:layout_height="180dp">
                 <androidx.constraintlayout.motion.widget.MotionLayout
                         android:id="@+id/motion_layout"
                         ... >
                     …
                 </androidx.constraintlayout.motion.widget.MotionLayout>
             </com.google.android.material.appbar.AppBarLayout>

             <androidx.core.widget.NestedScrollView
                     ...
                     app:layout_behavior="@string/appbar_scrolling_view_behavior" >
                     ...
             </androidx.core.widget.NestedScrollView>
          </androidx.coordinatorlayout.widget.CoordinatorLayout>

  This layout uses a CoordinatorLayout to share scrolling information
  between the NestedScrollView and the AppBarLayout. So, when the
  NestedScrollView scrolls up it will tell the AppBarLayout
  about the change. That's how you implement a collapsing
  toolbar like this on Android - the scrolling of the text
  will be "coordinated" with the collapsing header.

  The motion scene that @id/motion_layout points to is similar to
  the motion scene in the last step. However, the OnSwipe declaration
  was removed to enable it to work with CoordinatorLayout.

    3. Run the app and go to Step 8. You see that when you scroll the
       text, the moon does not move.

Make the MotionLayout scroll

`//TODO 1.17`
    1. To make the MotionLayout view scroll as soon as the NestedScrollView
       scrolls, add app:minHeight and app:layout_scrollFlags to the
       MotionLayout.

          <!-- layout/activity_step8.xml -->
          <!-- Add minHeight and layout_scrollFlags to the MotionLayout -->

          <androidx.constraintlayout.motion.widget.MotionLayout
                 android:id="@+id/motion_layout"
                 android:layout_width="match_parent"
                 android:layout_height="match_parent"
                 android:background="@drawable/m_eightyone"
                 app:layoutDescription="@xml/step8"
                 app:motionDebug="SHOW_PATH"
                 android:minHeight="80dp"
                 app:layout_scrollFlags="scroll|enterAlways|snap|exitUntilCollapsed">

    2. Run the app again and got to Step 8. You see that the MotionLayout
       collapses as you scroll up. However, the animation does not
       progress based on the scroll behavior yet.

Move the motion with code

`//TODO 1.18`
  Open Step8Activity.kt . Edit the coordinateMotion() function to tell
  MotionLayout about the changes in scroll position.

          // Step8Activity.kt
          // TODO: set progress of MotionLayout based on an
                   AppBarLayout.OnOffsetChangedListener

          val appBarLayout: AppBarLayout = findViewById(R.id.appbar_layout)
          val motionLayout: MotionLayout = findViewById(R.id.motion_layout)

          val listener = AppBarLayout.OnOffsetChangedListener { unused, verticalOffset ->
             val seekPosition = -verticalOffset / appBarLayout.totalScrollRange.toFloat()
             motionLayout.progress = seekPosition
          }

          appBarLayout.addOnOffsetChangedListener(listener)

  This code will register a OnOffsetChangedListener that will be called
  every time the user scrolls with the current scroll offset.

  MotionLayoutsupports seeking its transition by setting the progress
  property. To convert between a verticalOffset and a percentage
  progress, divide by the total scroll range.

  MotionLayout can seek to a specific point in the animation in code.

  Do this by setting motionLayout.progress. MotionLayout will
  immediately "jump" to the position that was specified.

  So, for example, if you set the progress to 0.43, MotionLayout will
  jump to 43% through the animation.

Try out the animation

  Deploy the app again and run the Step 8 animation. You see
  that MotionLayout will progress the animation based on the
  scroll position.

https://video.udacity-data.com/topher/2019/October/5d95142e_step8/step8.gif

  It's possible to build custom dynamic collapsing toolbar animations
  using MotionLayout. By using a sequence of KeyFrames you can
  achieve very bold effects.

  AppBarLayout does not resize the MotionLayout.

  The MotionLayout view will be moved partially offscreen when
  AppBarLayout collapses it. It will not be resized, but just
  moved up. If you have constraints to the top of the
  MotionLayout, they will be offscreen at the end of
  the animation. To work with AppBarLayout ensure
  end constraints are anchored to the bottom of
  the parent.
