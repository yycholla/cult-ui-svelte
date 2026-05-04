<script lang="ts">
	import { Spring } from 'svelte/motion';

	interface AnimatedNumberProps {
		/** Target numeric value to animate toward */
		value: number;
		/** Spring stiffness. Higher = snappier. Default 75 */
		stiffness?: number;
		/** Spring damping. Higher = less bounce. Default 15 */
		damping?: number;
		/** Decimal precision for the displayed value. Default 0 */
		precision?: number;
		/** Format function receives the animated number and returns a display string. Defaults to `toLocaleString()` */
		format?: (value: number) => string;
		/** CSS class(es) forwarded to the root span */
		class?: string;
	}

	let {
		value,
		stiffness = 75,
		damping = 15,
		precision = 0,
		format = (num: number) => num.toLocaleString(),
		class: className = ''
	}: AnimatedNumberProps = $props();

	// Svelte's Spring does not expose a `mass` parameter like framer-motion.
	// It supports stiffness/damping/precision, which cover the common cult-ui use case.
	const animatedValue = new Spring(0, { precision: 0.001 });

	$effect(() => {
		animatedValue.stiffness = stiffness;
		animatedValue.damping = damping;
		animatedValue.set(value);
	});

	let displayValue = $derived(format(parseFloat(animatedValue.current.toFixed(precision))));
</script>

<span class={className}>{displayValue}</span>
