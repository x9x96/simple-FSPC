 /*
 * Copyright (C) 2024 Simple Foldable Smartphone Power Control
 * by: Israel Oyetunji
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *      https://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

open class Phone(var isScreenLightOn: Boolean = false){
    fun switchOn() {
        isScreenLightOn = true
    }
    
    fun switchOff() {
        isScreenLightOn = false
    }
    
    fun checkPhoneScreenLight() {
        val phoneScreenLight = if (isScreenLightOn) "on" else "off"
        println("The phone screen's light is $phoneScreenLight.")
    }
}

class FoldablePhone(var isFolded: Boolean = true): Phone() {
	
    var powerButtonState = 0
    
    fun fold() {
        isFolded = true
        super.switchOff()
    }
    
    fun unfold() {
        isFolded = false
    }
    
    fun pressPowerButton() { 
        if (!isFolded) {
            if (powerButtonState == 0) {
                super.switchOn()
                powerButtonState++
            } else {
                super.switchOff()
                powerButtonState--
            }
            
        } else super.switchOff()
    }
    
}

fun main() {    
    val phoneAction = FoldablePhone()
    println("START running (6) tests")

    println("\n:::T_001: By default the phone's power button HAS NOT been pressed, so the inner screen should be off")
	phoneAction.checkPhoneScreenLight()   

    println("\n:::T_002: Power Button HAS been pressed")
	phoneAction.pressPowerButton()   
    println("::::: But by default the phone is also folded, so the inner screen should not turn on")
	phoneAction.checkPhoneScreenLight()   

    println("\n:::T_003: Phone HAS been unfolded")
	phoneAction.unfold()     
    println("::::: But Power Button HAS NOT been pressed, so the inner screen should still be off")
	phoneAction.checkPhoneScreenLight()   

    println("\n:::T_004: Phone IS still unfolded")
	phoneAction.pressPowerButton()   
    println("::::: NOW the Power Button HAS been pressed, so the inner screen should turn on")
	phoneAction.checkPhoneScreenLight()   
    
    println("\n:::T_005: Phone IS still unfolded AND the inner screen IS still on")    
    phoneAction.pressPowerButton()
    println("::::: NOW the Power Button HAS been pressed again, so the inner screen should turn off")
	phoneAction.checkPhoneScreenLight()   

    println("\n::::: Phone IS still unfolded")
	phoneAction.pressPowerButton()   
    println("::::: AND Power Button HAS been pressed once more, so the inner screen should turn on")
	phoneAction.checkPhoneScreenLight()   
    
    println("\n:::T_006: Phone HAS been folded, so the inner screen should not turn off automatically")    
    phoneAction.fold()
	phoneAction.checkPhoneScreenLight()

    println("\nEND running (6) tests")
    println("Other tests persists, though not tangible to this context")    
}
