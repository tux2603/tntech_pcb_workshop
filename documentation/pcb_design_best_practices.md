# Best Practices for PCB Designs

## 1. Designing with manufacturability and assembly in mind

A PCB isn't terribly useful if it only exists as some ones and zeroes on your computer. At every stage of the design process, you should be thinking about how your design will be manufactured, and if anything you're doing will make it difficult or impossible to produce. 

### 1.1 Design rules and other manufacturing considerations

- **Pick a target manufacturer early.** Every manufacturer has slightly different capabilities, which will affect many design decisions you make as you design the PCB. By picking a manufacturer early, you can make sure that your design is compatible with their capabilities, and avoid having to rework your design later.

- **Set up your design rules to match the capabilities of your manufacturer.** This is one of the most important steps in PCB design, and should be done before you start layout or routing. this includes minimum trace width and spacing, via sizes, and what sorts of vias are supported. Manufacturers can not reliably produce a PCB that violates their design rules, so if you don't set up your design rules correctly, you will almost certainly have to go back and rework your design before it can be manufactured. This sort of rework can be very time consuming and frustrating, so it's best to avoid it by setting up your design rules correctly from the start and checking them frequently as you work on your design.

- **Pick a stack-up early and stick with it.** A stack-up is the arrangement of copper and insulating layers in your PCB, along with a plan for how each copper layer will be used. The stack-up will affect the electrical performance of your design, the required traced widths for impedance-controlled signals, how easy it is to route your design, and the overall cost of manufacturing. Stack-ups will typically have one or more signal layers, each with a corresponding ground plane, and potentially one or more power planes. 

- **Avoid using the extreme limits of your manufacturer's capabilities when it's not necessary**. The capabilities of your manufacturer are only an absolute limit to what can be done. Just because your manufacturer can make 4 mil wide traces with 4 mil spacing doesn't mean that all your traces should be that small. Unless there is a specific reason to use a certain width trace, there's no reason to make your traces as small as possible. Wider traces are easier to manufacture, are more robust, and are easier to fix if something goes wrong. Set your default trace width to something reasonable, like 0.2-0.3 mm (~10 mil), and only use smaller traces when you have a reason to do so. Similarly, don't use the smallest possible via sizes unless you have a reason to do so.

- **Don't use high-end features like blind vias or super fine pitch traces unless you are sure that you need them for a design.** High-end features likes these can make a complex design possible, but will also cause the cost of manufacturing to skyrocket. If you can get away with the "lowest-tier" capabilities of your manufacturer, you should.

### 1.2 Component and footprint selection

- **Select components and footprints that are realistic for your assembly method.** If you are hand soldering, do not use tiny 0201 components. You _technically_ can solder them by hand, but it will be a nightmare. Through-hole components are easier to solder by hand, but they take up more space and are often more expensive.

- **Make sure that you have the right footprint for your selected components.** Components are often available in multiple different package types, each of which will require a different footprint on your PCB. Make sure that the footprint you are using matches the package type of the component that your are buying. If you are using a footprint that you found online, make sure to double check the dimensions of the footprint against the datasheet for the component to make sure that it is correct. 

- **Avoid using components that are difficult or cumbersome to source.** Doing this well takes a little experience, but you can get a basic idea of what is easy to source by looking at the stock levels and lifecycle of the components you are considering. If one option has 10,000 units in stock and another has 10, it is very likely that the first option will be more reliable to source in the long run. Similarly, if a component is marked as something like "End of Life," "Obsolete, "or "Not Recommended for New Designs", it will be extremely difficult to source in the future, and you should avoid using it if at all possible.

- **Avoid "Marketplace" style vendors when possible.** On sites like Digikey and Mouser, there are often "Marketplace" parts available at a lower price. These parts are typically sold and shipped by third-party sellers. They can potentially bring the overall cost of your design down, but will often have longer shipping times and require you to pay separate shipping charges. If you are on a tight schedule, it is often better to avoid marketplace parts.

### 1.3 Assembly considerations

- **Make sure that the pads for your components are on the correct layers.** You can't solder a component to a pad that is in the middle of a PCB. This means that your pads must be on either the top or bottom layer unless you are doing a very complex and extremely expensive custom designs.

- **Prefer to keep surface mount parts all on the same side of the board.** Single-sided assembly is cheaper and easier than double-sided assembly. If it doesn't matter what side of a board a component is on, pick a default side and stick with it. Typically the top layer is the standard for surface mount parts, but if it makes more sense to you to put everything on the bottom, that's fine too. Just make sure that you are consistent.

- **Avoid placing components too close together.** If components are too close together it can be extremely difficult to solder them, especially if you are hand soldering. Keep a reasonable buffer between components.

- **Avoid placing components too close to the edge of the board.** If components are too close to the edge of the board, they can be damaged during assembly or when the board is being handled. Unless your component needs to be on the edge of the board, for example if it's a connector or a button, keep them a reasonable distance back.


## 2. Designing with electrical performance in mind

While low-speed, low-power designs can often get away with a lot of "sloppy" design practices, high-speed or high-power designs will require careful attention to detail in order to function correctly. Even if your design is low-speed and low-power, it is still a good idea to follow best practices for electrical performance in order to form good habits that will carry over to more complex designs in the future.

### 2.1 Power distribution

- **Use a ground plane.** A ground plane is a large area of copper that is connected to the ground net of your design. A ground plane provides a reliable, low-impedance return path for signals and will make your design more robust to noise and interference and (hopefully) easier to route. On 4+ layer boards, it is extremely common to dedicate one or more entire layers to a solid ground plane. On 2-layer boards, it is a bit harder to dedicate an entire layer to a ground plane, but it is still extremely common to have one layer be mostly ground with as few other traces as possible. I can not stress enough how useful a ground plane is. Use a ground plane.

- **Use a "star" topology instead of a "daisy chain" topology for power distribution as much as possible.** A star topology is one where all the power connections to your components fan out from a single point, while a daisy chain topology is one where the power connections to your components are connected with a single trace, one after the other. A daisy chain topology will typically be easier to route, so it can be very tempting to use, but it can cause problems with accumulating voltage drops and noise as power travels down the chain. A star topology will typically require a bit more routing work, but will provide your components with a more stable and reliable power supply.

- **Use proper trace thicknesses based on your power needs.** If you are designing a high-power circuit, it is important to use traces that are thick enough to handle the current without overheating or causing voltage drops. There are many online calculators available that can help you determine the appropriate trace width based on the current and the thickness of your PCB copper layer.

- **Use decoupling capacitors near your ICs.** ICs will often draw large spikes of current as they switch states, which can cause glitches and brown-outs if your power distribution network isn't able to supply that current quickly enough. Decoupling capacitors are small capacitors placed as close to an IC's power pins as possible, and act as a local reservoir of charge that can supply the IC with power during these spikes. A good rule of thumb is to use a 0.1uF (100nF) ceramic capacitor for each power pin of an IC unless the IC's datasheet specifies otherwise. Connect one end of the decoupling capacitor to the IC's power pin, and connect the other end to the nearest ground plane.

### 2.2 Signal integrity

- **Route traces carrying your fastest/most sensitive signals first.** High-speed and impedance controlled signals will typically have the strictest routing requirements, so it is a good idea to get them out of the way first. Once you get traces routed for your high-speed signals, you can move on to routing traces for the rest of your signals.

- **Reference high-speed signals to an uninterrupted ground plane.** Anytime you have a current flowing through a trace, there must be a corresponding current flowing back to the source. If that current doesn't exist, it means that KCL is messed up and the universe has broken. Once the frequency components of a signal get high enough, this return current will no longer just follow the path of least resistance, but will instead follow the path of least impedance. The means that when you have a high-speed signal traveling along a trace, the return current will want to flow directly below that trace through the ground plane. If there is no ground plane below the trace or if the ground plane is interrupted by a gap, hole, or some other trace running through it, the return current will have to find some other path back to the source. This path is incredibly hard to predict, and can cause all sorts of problems with signal integrity, including reflections, crosstalk, and EMI.

- **Prefer referencing low-speed signals to a ground plane.** Low speed signals are not as sensitive to signal integrity issues as high-speed signals, but it is still a good idea to reference them to a ground plane whenever possible. It is possible to reference them to a power plane if a design requires it, but this is not ideal. If you do reference a low-speed signal to a power plane, make sure that you have decoupling capacitors close to the signal's source and load to complete the return path for the signal.

- **Use appropriate trace widths for impedance-controlled signals.** The width and spacing of a trace will affect the impedance that it presents to signals traveling along it. If you have an impedance mismatch between a trace carrying a high-speed signal and the source or load that it is connected to, you will get reflections and other signal integrity issues. Calculate the required trace width and spacing for your impedance controlled signals based on your PCB stack-up before you start routing, and make sure to use those widths and spacings when routing those traces.

- **Route differential pairs together and maintain their spacing.** Differential pairs are sets of two traces that carry a set of complementary signals. Differential pairs are often used for high-speed signals because they offer better noise immunity and produce less noise themselves. When routing differential pairs, it is important to keep the two traces close together and maintain a consistent spacing between them. 



## 3. Designing with testing and debugging in mind

### 3.1 Test points and indicators

- **Include indicator LEDs in your design.** In almost every situation, it is a good idea to include indicator LEDs in your design. LEDs, especially surface-mount LEDs, are extremely cheap and can provide an easy visual indicator of things like power, status, and detected errors. If you have any sort of power regulation in your design, it is a good idea to include a power indicator LED. If your design is using some for of microcontroller, it is a good idea to use spare GPIO pins from that microcontroller to drive status LEDs. It's a lot faster to glance at a board and see that an LED is lit or blinking than it is to grab a multimeter or oscilloscope and start probing around to try and figure out what is going on.

- **Include test points for important nets on your PCB.** While status LEDs are useful, you sometimes do need a bit more information than a simple on/off indicator can provide. In these situations, it is a good idea to include test points in your design. Test points are small pads that are connected to important signals or power planes, and provide a convenient place to probe with a multimeter or oscilloscope

### 3.2 Documentation

- **Keep track of design decisions and changes.** Documenting your design decisions and any changes made during the design process is crucial for maintaining a clear understanding of the design and for future reference. You don't want to go back to your design a few weeks later and try to remember if there was a reason you're using a 19k resistor, or if it was just a typo.

- **Use silkscreen labels as much as possible** Silkscreen labels are the text and symbols printed on the surface of your PCB. They can be used to label components, indicate pin numbers, and provide other useful information. If you have extra space, mark down what pins are being used for what purpose, or any other useful information. This will make it easier to debug your design later, and will also make it easier for someone else to understand your design if they need to work on it in the future.

- **Use version control for your PCB design files.** Version control, such as git, is a system that makes it easy to track changes to files over time. Using version control will not only provide an overview of the changes you've made over time, but will also make it easier to revert to a previous version of your design if you make a mistake or decide that the changes you made weren't actually necessary. 

### 3.3 "Flexible" design

- **Design your PCB to be easily modified post-manufacturing.** Chances are the first iteration of a PCB design will not be perfect, and you'll likely have to make some tweaks. For prototypes, you can work in some design elements to make these tweaks easier. Typically, this will mean leaving some extra space around components, using thicker traces, providing test pads for important nets, and avoiding routing signals on internal layers. Copper is effectively free on a PCB, so there's not much reason to be stingy with it. If you have the space, use it to make your design easier to tweak.





