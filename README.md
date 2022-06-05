# cudaQueue

- Queue Datastructure for Nvidia Cuda Devices.
- Optimized all memory is allocated on Cuda Device for optimal use.
- Usable in device code



EXAMPLE:
```

template <typename T>
__device__ inline void print(cudaQueue<T>& value) {
	int size = value.size();
	for (int var = 0; var < size; ++var) {
		printf("%i\n", value.front());
		value.pop();
    }
}

__device__ inline void fillQueue() {
	cudaQueue<int> var;
	for (int i = 0; i < 15; ++i) {
		var.push(i * 14 + 1);
	}
	print(var);
}

__global__ void value() {
	fillQueue();
}



int main()
{
	value <<< 1, 1 >>> ();
	cudaDeviceSynchronize();
	cudaDeviceReset();
}

```
